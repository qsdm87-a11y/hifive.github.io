<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HiFiVE - Language Exchange</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">

<style>
:root {
  --bg: #0d0f14;
  --bg2: #13161e;
  --bg3: #1a1e2a;
  --card: #1e2230;
  --border: #2a2f40;
  --accent: #4A90E2;
  --accent2: #7B61FF;
  --accent3: #00d4a0;
  --text: #e8eaf0;
  --text2: #8b90a4;
  --text3: #555c73;
  --danger: #ff4d6a;
  --success: #00d4a0;
  --radius: 14px;
  --radius-sm: 8px;
  --shadow: 0 8px 32px rgba(0,0,0,0.4);
  --glow: 0 0 20px rgba(74,144,226,0.25);
}
* { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: 'DM Sans', sans-serif; background: #f5f5f5; color: var(--text); min-height: 100vh; overflow-x: hidden; display: flex; justify-content: center; align-items: center; }

#phone-frame {
  width: 375px;
  height: 667px;
  background: #000;
  border-radius: 30px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(0,0,0,0.5);
}

#phone-frame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 150px;
  height: 30px;
  background: #000;
  border-radius: 0 0 20px 20px;
  z-index: 1;
}
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
.hidden { display: none !important; }

/* TOAST */
.toast {
  position: fixed; bottom: 80px; left: 50%; transform: translateX(-50%);
  background: var(--card); border: 1px solid var(--border); color: var(--text);
  padding: 10px 20px; border-radius: 20px; font-size: 0.88rem;
  z-index: 9999; animation: toastIn 0.3s ease, toastOut 0.3s ease 2.4s forwards;
  pointer-events: none; white-space: nowrap; box-shadow: var(--shadow);
}
@keyframes toastIn { from { opacity:0; transform: translateX(-50%) translateY(10px); } to { opacity:1; transform: translateX(-50%) translateY(0); } }
@keyframes toastOut { to { opacity:0; transform: translateX(-50%) translateY(10px); } }

/* MODAL */
.modal-overlay {
  position: fixed; inset: 0; z-index: 1000;
  background: rgba(0,0,0,0.75); backdrop-filter: blur(8px);
  display: flex; align-items: center; justify-content: center;
  animation: fadeIn 0.2s ease;
}
@keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
@keyframes slideUp { from { opacity:0; transform: translateY(24px); } to { opacity:1; transform: translateY(0); } }
.modal-box {
  background: var(--bg2); border: 1px solid var(--border); border-radius: var(--radius);
  width: 100%; max-width: 440px; margin: 16px; box-shadow: var(--shadow);
  animation: slideUp 0.25s ease; max-height: 90vh; overflow-y: auto;
}
.modal-head {
  display: flex; align-items: center; justify-content: space-between;
  padding: 20px 24px 16px; border-bottom: 1px solid var(--border);
}
.modal-head h2 { font-family: 'Syne', sans-serif; font-size: 1.25rem; font-weight: 700; }
.modal-close {
  width: 32px; height: 32px; background: var(--bg3); border: none; border-radius: 50%;
  color: var(--text2); cursor: pointer; font-size: 1.1rem;
  display: flex; align-items: center; justify-content: center; transition: all 0.2s;
}
.modal-close:hover { background: var(--danger); color: #fff; }
.modal-body { padding: 24px; }

/* FORMS */
.form-group { margin-bottom: 16px; }
.form-group label { display: block; font-size: 0.82rem; color: var(--text2); margin-bottom: 6px; font-weight: 500; letter-spacing: 0.3px; }
.form-group input, .form-group select, .form-group textarea {
  width: 100%; padding: 11px 14px; background: var(--bg3); border: 1px solid var(--border);
  border-radius: var(--radius-sm); color: var(--text); font-family: 'DM Sans', sans-serif;
  font-size: 0.9rem; outline: none; transition: border-color 0.2s, box-shadow 0.2s;
}
.form-group input:focus, .form-group select:focus, .form-group textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(74,144,226,0.15); }
.form-group select option { background: var(--bg3); }
.auth-btn {
  width: 100%; padding: 12px;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  border: none; border-radius: var(--radius-sm); color: #fff;
  font-family: 'DM Sans', sans-serif; font-size: 0.95rem; font-weight: 600;
  cursor: pointer; margin-top: 4px; transition: opacity 0.2s, transform 0.1s;
}
.auth-btn:hover { opacity: 0.9; transform: translateY(-1px); }
.auth-btn:active { transform: translateY(0); }
.auth-switch { text-align: center; margin-top: 16px; font-size: 0.85rem; color: var(--text2); }
.auth-switch a { color: var(--accent); text-decoration: none; font-weight: 500; }
.auth-switch a:hover { text-decoration: underline; }
.form-error { color: var(--danger); font-size: 0.82rem; margin-top: 6px; }

/* APP SHELL */
.app { display: flex; flex-direction: column; height: 100%; position: absolute; top: 30px; left: 0; right: 0; bottom: 0; border-radius: 0 0 30px 30px; overflow: hidden; }

/* TOP BAR */
.topbar {
  display: flex; align-items: center; justify-content: space-between;
  padding: 14px 20px; background: var(--bg2); border-bottom: 1px solid var(--border);
  position: sticky; top: 0; z-index: 100;
}
.topbar-logo {
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.3rem;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; letter-spacing: -0.5px;
}
.topbar-user { display: flex; align-items: center; gap: 12px; }
.topbar-name { font-size: 0.88rem; color: var(--text2); }
.btn-sm { padding: 7px 14px; border-radius: 20px; font-size: 0.82rem; font-family: 'DM Sans', sans-serif; font-weight: 500; cursor: pointer; transition: all 0.2s; border: none; }
.btn-outline { background: transparent; border: 1px solid var(--border); color: var(--text2); }
.btn-outline:hover { border-color: var(--accent); color: var(--accent); }
.btn-primary { background: linear-gradient(135deg, var(--accent), var(--accent2)); color: #fff; }
.btn-primary:hover { opacity: 0.88; }
.btn-danger { background: var(--danger); color: #fff; }
.btn-danger:hover { opacity: 0.85; }

/* MAIN */
.main { flex: 1; overflow-y: auto; }

/* SCREENS */
.screen { display: none; }
.screen.active { display: block; }

/* LANDING */
#screen-landing {
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  min-height: calc(100vh - 57px); text-align: center; padding: 20px 20px 30px;
  position: relative; overflow: hidden; background: var(--bg);
}
.landing-bg { position: absolute; inset: 0; pointer-events: none; overflow: hidden; }
.landing-bg-blob { position: absolute; border-radius: 50%; filter: blur(80px); opacity: 0.08; }
.blob1 { width: 400px; height: 400px; background: var(--accent); top: -100px; left: -100px; }
.blob2 { width: 300px; height: 300px; background: var(--accent2); bottom: -80px; right: -80px; }

/* APP LOGO */
.app-logo-wrap {
  display: flex; align-items: center; gap: 12px; margin-bottom: 16px; z-index: 2; position: relative;
  animation: logoFadeIn 0.8s ease both;
}
@keyframes logoFadeIn { from { opacity:0; transform: translateY(-12px); } to { opacity:1; transform: translateY(0); } }
.app-logo-icon {
  width: 56px; height: 56px; border-radius: 16px;
  background: linear-gradient(135deg, #1a3a6b 0%, #2563eb 50%, #7B61FF 100%);
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 0 0 1px rgba(74,144,226,0.3), 0 8px 24px rgba(37,99,235,0.4);
  position: relative; overflow: hidden; flex-shrink: 0;
}
.app-logo-icon::before {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.18) 0%, transparent 60%);
}
.app-logo-icon svg { width: 32px; height: 32px; position: relative; z-index: 1; }
.app-logo-text { text-align: left; }
.app-logo-name {
  font-family: 'Syne', sans-serif; font-size: 1.6rem; font-weight: 800; letter-spacing: -0.5px;
  background: linear-gradient(135deg, #60a5fa, #818cf8, #a78bfa);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; line-height: 1;
}
.app-logo-sub { font-size: 0.7rem; color: var(--text3); letter-spacing: 1.5px; text-transform: uppercase; margin-top: 2px; }

/* 3D EARTH */
.earth-container {
  width: 190px; height: 190px; position: relative; margin-bottom: 18px; z-index: 2;
  animation: earthReveal 1.2s cubic-bezier(0.16,1,0.3,1) both;
}
@keyframes earthReveal { from { opacity:0; transform: scale(0.7); } to { opacity:1; transform: scale(1); } }
#earth-canvas { width: 190px; height: 190px; border-radius: 50%; display: block; }
.earth-glow {
  position: absolute; inset: -20px; border-radius: 50%;
  background: radial-gradient(circle, rgba(37,99,235,0.2) 0%, transparent 70%);
  pointer-events: none; animation: glowPulse 3s ease-in-out infinite;
}
.earth-ring {
  position: absolute; inset: -8px; border-radius: 50%;
  border: 1px solid rgba(74,144,226,0.2);
  animation: ringRotate 8s linear infinite;
}
.earth-ring::before {
  content: ''; position: absolute; top: 50%; left: -4px;
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--accent); transform: translateY(-50%);
  box-shadow: 0 0 8px var(--accent);
}
@keyframes glowPulse { 0%,100% { opacity:0.6; } 50% { opacity:1; } }
@keyframes ringRotate { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

#screen-landing h1 {
  font-family: 'Syne', sans-serif; font-size: 2.2rem; font-weight: 800;
  background: linear-gradient(135deg, var(--accent), var(--accent2));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 8px;
  display: none;
}
#screen-landing > p { color: var(--text2); font-size: 0.95rem; max-width: 320px; margin-bottom: 10px; line-height: 1.6; z-index:2; position:relative; }
.landing-tagline { font-size: 0.82rem; color: var(--text3); margin-bottom: 28px !important; }
.landing-btns { display: flex; gap: 14px; flex-wrap: wrap; justify-content: center; z-index:2; position:relative; }
.landing-btn-main { padding: 13px 32px; border-radius: 50px; font-size: 1rem; font-weight: 600; font-family: 'DM Sans', sans-serif; cursor: pointer; transition: all 0.2s; }
.landing-btn-signin { background: transparent; border: 2px solid var(--accent); color: var(--accent); }
.landing-btn-signin:hover { background: rgba(74,144,226,0.1); }
.landing-btn-signup { background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; color: #fff; box-shadow: var(--glow); }
.landing-btn-signup:hover { opacity: 0.88; transform: translateY(-2px); }
.landing-perks { display: flex; gap: 10px; margin-top: 28px; flex-wrap: wrap; justify-content: center; z-index:2; position:relative; }
.landing-perk { display: flex; align-items: center; gap: 8px; font-size: 0.82rem; color: var(--text3); }
.landing-perk-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent3); flex-shrink: 0; }

/* BOTTOM NAV */
.bottom-nav { display: flex; background: var(--bg2); border-top: 1px solid var(--border); position: sticky; bottom: 0; z-index: 100; }
.nav-item { flex: 1; display: flex; flex-direction: column; align-items: center; padding: 10px 6px; gap: 4px; background: none; border: none; cursor: pointer; color: var(--text3); font-size: 0.72rem; font-family: 'DM Sans', sans-serif; transition: color 0.2s; position: relative; }
.nav-item .nav-icon { font-size: 1.35rem; transition: transform 0.2s; }
.nav-item:hover { color: var(--text2); }
.nav-item:hover .nav-icon { transform: translateY(-2px); }
.nav-item.active { color: var(--accent); }
.nav-item.active::before { content: ''; position: absolute; top: 0; left: 20%; right: 20%; height: 2px; background: linear-gradient(90deg, var(--accent), var(--accent2)); border-radius: 0 0 4px 4px; }

/* SECTION HEADERS */
.section-header { padding: 24px 20px 16px; }
.section-header h2 { font-family: 'Syne', sans-serif; font-size: 1.4rem; font-weight: 700; }
.section-header p { color: var(--text2); font-size: 0.88rem; margin-top: 4px; }

/* TALK ROOMS */
.room-list { padding: 0 16px 16px; display: flex; flex-direction: column; gap: 12px; }
.room-card { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px 18px; cursor: pointer; transition: all 0.2s; display: flex; align-items: center; justify-content: space-between; }
.room-card:hover { border-color: var(--accent); transform: translateY(-2px); box-shadow: 0 4px 20px rgba(0,0,0,0.3); }
.room-card-left { display: flex; flex-direction: column; gap: 6px; }
.room-card-name { font-weight: 600; font-size: 1rem; }
.room-card-meta { display: flex; gap: 10px; flex-wrap: wrap; }
.tag { padding: 3px 10px; border-radius: 20px; font-size: 0.75rem; font-weight: 500; background: rgba(74,144,226,0.12); color: var(--accent); border: 1px solid rgba(74,144,226,0.2); }
.tag.tag-green { background: rgba(0,212,160,0.1); color: var(--accent3); border-color: rgba(0,212,160,0.2); }
.tag.tag-purple { background: rgba(123,97,255,0.1); color: var(--accent2); border-color: rgba(123,97,255,0.2); }
.room-card-count { text-align: right; }
.room-count-num { font-size: 1.2rem; font-weight: 700; color: var(--accent2); }
.room-count-label { font-size: 0.72rem; color: var(--text3); }

/* ACTIVE ROOM */
.active-room { padding: 16px; display: flex; flex-direction: column; gap: 16px; }
.room-topbar { display: flex; align-items: center; gap: 12px; background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px 18px; }
.room-topbar-info h3 { font-weight: 700; font-size: 1.05rem; }
.room-topbar-info p { color: var(--text2); font-size: 0.82rem; }
.back-btn { background: var(--bg3); border: 1px solid var(--border); border-radius: 8px; color: var(--text2); cursor: pointer; padding: 8px 14px; font-size: 0.85rem; font-family: 'DM Sans', sans-serif; transition: all 0.2s; white-space: nowrap; }
.back-btn:hover { border-color: var(--accent); color: var(--accent); }
.stage-area { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px; }
.stage-title { font-size: 0.8rem; color: var(--text2); font-weight: 600; letter-spacing: 0.5px; text-transform: uppercase; margin-bottom: 14px; }
.stage-avatars { display: flex; flex-wrap: wrap; gap: 14px; }
.stage-avatar { display: flex; flex-direction: column; align-items: center; gap: 6px; cursor: pointer; }
.avatar-circle { width: 52px; height: 52px; border-radius: 50%; background: linear-gradient(135deg, var(--accent), var(--accent2)); display: flex; align-items: center; justify-content: center; font-size: 1.3rem; position: relative; border: 2px solid transparent; transition: all 0.2s; }
.avatar-circle:hover { transform: scale(1.05); border-color: var(--accent); }
.avatar-circle.speaking { border-color: var(--accent3); box-shadow: 0 0 16px rgba(0,212,160,0.4); }
.avatar-circle.muted::after { content: '🔇'; font-size: 0.7rem; position: absolute; bottom: -2px; right: -2px; background: var(--bg2); border-radius: 50%; padding: 2px; }
.avatar-name { font-size: 0.72rem; color: var(--text2); text-align: center; }
.audience-area { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px; }
.audience-grid { display: flex; flex-wrap: wrap; gap: 10px; margin: 12px 0; }
.audience-chip { display: flex; align-items: center; gap: 7px; background: var(--bg3); border: 1px solid var(--border); border-radius: 20px; padding: 6px 12px; font-size: 0.82rem; }
.audience-chip .dot { width: 7px; height: 7px; border-radius: 50%; background: var(--accent3); }
.raise-hand-btn { padding: 10px 20px; background: rgba(74,144,226,0.1); border: 1px solid var(--accent); border-radius: 20px; color: var(--accent); font-size: 0.9rem; font-family: 'DM Sans', sans-serif; cursor: pointer; transition: all 0.2s; }
.raise-hand-btn:hover { background: rgba(74,144,226,0.2); }
.raise-hand-btn.raised { background: rgba(255,77,106,0.1); border-color: var(--danger); color: var(--danger); }
.chat-panel { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px; display: flex; flex-direction: column; height: 260px; }
.chat-msgs { flex: 1; overflow-y: auto; display: flex; flex-direction: column; gap: 8px; padding-right: 4px; }
.chat-msg { display: flex; gap: 8px; }
.chat-msg-avatar { width: 28px; height: 28px; border-radius: 50%; background: linear-gradient(135deg, var(--accent2), var(--accent)); display: flex; align-items: center; justify-content: center; font-size: 0.8rem; flex-shrink: 0; }
.chat-msg-body { flex: 1; }
.chat-msg-name { font-size: 0.72rem; color: var(--accent); font-weight: 600; margin-bottom: 2px; }
.chat-msg-text { font-size: 0.85rem; color: var(--text); line-height: 1.4; }
.chat-msg-time { font-size: 0.7rem; color: var(--text3); }
.chat-input-row { display: flex; gap: 8px; margin-top: 12px; }
.chat-input-row input { flex: 1; padding: 10px 14px; background: var(--bg3); border: 1px solid var(--border); border-radius: 20px; color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 0.88rem; outline: none; }
.chat-input-row input:focus { border-color: var(--accent); }
.chat-send-btn { padding: 10px 18px; background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; border-radius: 20px; color: #fff; cursor: pointer; font-size: 0.88rem; font-weight: 500; font-family: 'DM Sans', sans-serif; transition: opacity 0.2s; }
.chat-send-btn:hover { opacity: 0.85; }
.emoji-btn2 { background: var(--bg3); border: 1px solid var(--border); border-radius: 20px; padding: 10px 12px; cursor: pointer; font-size: 1rem; }
.emoji-relative { position: relative; }
.emoji-picker-wrap { position: absolute; bottom: 44px; right: 0; background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 10px; display: grid; grid-template-columns: repeat(4, 1fr); gap: 6px; z-index: 200; box-shadow: var(--shadow); }
.emoji-pick { background: none; border: none; cursor: pointer; font-size: 1.1rem; padding: 4px; border-radius: 6px; transition: background 0.15s; }
.emoji-pick:hover { background: var(--bg3); }

/* CREATE ROOM BTN */
.create-room-btn { margin: 0 16px 16px; padding: 13px; background: linear-gradient(135deg, rgba(74,144,226,0.1), rgba(123,97,255,0.1)); border: 1px dashed var(--accent); border-radius: var(--radius); color: var(--accent); font-size: 0.92rem; font-weight: 600; font-family: 'DM Sans', sans-serif; cursor: pointer; transition: all 0.2s; display: flex; align-items: center; justify-content: center; gap: 8px; }
.create-room-btn:hover { background: rgba(74,144,226,0.15); }

/* CONNECT */
.connect-wrap { padding: 0 16px 16px; }
.connect-grid { display: flex; flex-direction: column; gap: 12px; }
.connect-card { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px 18px; cursor: pointer; transition: all 0.2s; display: flex; align-items: center; gap: 16px; }
.connect-card:hover { border-color: var(--accent); transform: translateY(-2px); box-shadow: 0 4px 20px rgba(0,0,0,0.3); }
.connect-avatar { width: 52px; height: 52px; border-radius: 50%; background: linear-gradient(135deg, var(--accent), var(--accent2)); display: flex; align-items: center; justify-content: center; font-size: 1.5rem; flex-shrink: 0; }
.connect-info { flex: 1; }
.connect-name { font-weight: 600; font-size: 0.95rem; margin-bottom: 4px; }
.connect-meta { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 4px; }
.connect-status { font-size: 0.78rem; color: var(--accent3); }
.connect-status.away { color: var(--text3); }

/* CONNECT PANEL */
.connect-panel-overlay { position: fixed; inset: 0; z-index: 500; background: rgba(0,0,0,0.6); backdrop-filter: blur(4px); display: flex; align-items: flex-end; justify-content: center; }
.connect-panel { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--radius) var(--radius) 0 0; width: 100%; max-width: 520px; padding: 24px; max-height: 80vh; overflow-y: auto; animation: slideUp 0.25s ease; }
.connect-panel-head { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 16px; }
.connect-panel-info h3 { font-family: 'Syne', sans-serif; font-size: 1.15rem; font-weight: 700; }
.connect-panel-info p { color: var(--text2); font-size: 0.85rem; margin-top: 2px; }
.connect-panel-meta { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 14px; }
.connect-actions-row { display: flex; gap: 10px; }
.follow-btn { padding: 10px 16px; background: rgba(74,144,226,0.1); border: 1px solid var(--accent); border-radius: 20px; color: var(--accent); font-family: 'DM Sans', sans-serif; font-size: 0.88rem; cursor: pointer; transition: all 0.2s; }
.follow-btn:hover { background: rgba(74,144,226,0.2); }
.follow-btn.following { background: rgba(0,212,160,0.1); border-color: var(--accent3); color: var(--accent3); }
.msg-btn { padding: 10px 16px; background: rgba(123,97,255,0.1); border: 1px solid var(--accent2); border-radius: 20px; color: var(--accent2); font-family: 'DM Sans', sans-serif; font-size: 0.88rem; cursor: pointer; transition: all 0.2s; }
.msg-btn:hover { background: rgba(123,97,255,0.2); }
.connect-chat { margin-top: 16px; }
.connect-chat h4 { font-size: 0.88rem; color: var(--text2); margin-bottom: 10px; }
.connect-msgs { height: 160px; overflow-y: auto; display: flex; flex-direction: column; gap: 8px; margin-bottom: 10px; }

/* HIFIVE */
.hifive-wrap { padding: 16px; max-width: 560px; margin: 0 auto; }
.hifive-hero { background: linear-gradient(135deg, rgba(74,144,226,0.08), rgba(123,97,255,0.08)); border: 1px solid var(--border); border-radius: var(--radius); padding: 28px; text-align: center; margin-bottom: 16px; }
.hifive-hero h3 { font-family: 'Syne', sans-serif; font-size: 1.3rem; font-weight: 700; margin-bottom: 10px; }
.hifive-hero p { color: var(--text2); font-size: 0.88rem; line-height: 1.6; max-width: 320px; margin: 0 auto 20px; }
.hifive-start-btn { padding: 12px 28px; background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; border-radius: 30px; color: #fff; font-family: 'DM Sans', sans-serif; font-size: 0.95rem; font-weight: 600; cursor: pointer; transition: all 0.2s; }
.hifive-start-btn:hover { opacity: 0.88; transform: translateY(-2px); }
.hifive-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 16px; }
.hifive-stat-card { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px; text-align: center; }
.hifive-stat-num { font-family: 'Syne', sans-serif; font-size: 2rem; font-weight: 800; background: linear-gradient(135deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.hifive-stat-label { font-size: 0.78rem; color: var(--text2); margin-top: 4px; }
.leaderboard { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px; }
.leaderboard h3 { font-family: 'Syne', sans-serif; font-size: 1rem; margin-bottom: 14px; }
.lb-row { display: flex; align-items: center; gap: 12px; padding: 10px 0; border-bottom: 1px solid var(--border); }
.lb-row:last-child { border-bottom: none; }
.lb-rank { font-size: 1.2rem; width: 32px; text-align: center; }
.lb-rank.gold { color: #FFD700; }
.lb-rank.silver { color: #C0C0C0; }
.lb-rank.bronze { color: #CD7F32; }
.lb-name { flex: 1; font-weight: 500; }
.lb-pts { font-size: 0.88rem; color: var(--accent2); font-weight: 600; }

/* PROFILE */
.profile-wrap { padding: 20px 16px; max-width: 560px; margin: 0 auto; }
.profile-card { background: var(--card); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; margin-bottom: 16px; }
.profile-card-header { padding: 24px; display: flex; align-items: center; gap: 18px; border-bottom: 1px solid var(--border); background: linear-gradient(135deg, rgba(74,144,226,0.06), rgba(123,97,255,0.06)); }
.profile-avatar-big { width: 72px; height: 72px; border-radius: 50%; flex-shrink: 0; background: linear-gradient(135deg, var(--accent), var(--accent2)); display: flex; align-items: center; justify-content: center; font-size: 2rem; border: 3px solid var(--border); position: relative; overflow: hidden; cursor: pointer; }
.profile-avatar-big img { width: 100%; height: 100%; object-fit: cover; }
.profile-avatar-big .upload-overlay { position: absolute; inset: 0; background: rgba(0,0,0,0.5); display: none; align-items: center; justify-content: center; font-size: 1.2rem; }
.profile-avatar-big:hover .upload-overlay { display: flex; }
.profile-main-info { flex: 1; }
.profile-main-info h3 { font-family: 'Syne', sans-serif; font-size: 1.2rem; font-weight: 700; margin-bottom: 4px; }
.profile-langs { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 8px; }
.profile-status { display: flex; align-items: center; gap: 6px; font-size: 0.82rem; color: var(--accent3); }
.status-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--accent3); display: inline-block; }
.profile-edit-btn { padding: 8px 16px; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--radius-sm); color: var(--text2); font-family: 'DM Sans', sans-serif; font-size: 0.85rem; cursor: pointer; transition: all 0.2s; flex-shrink: 0; }
.profile-edit-btn:hover { border-color: var(--accent); color: var(--accent); }
.profile-card-body { padding: 0 24px 24px; }
.profile-field { padding: 14px 0; border-bottom: 1px solid var(--border); }
.profile-field:last-child { border-bottom: none; }
.profile-field label { font-size: 0.78rem; color: var(--text3); font-weight: 600; letter-spacing: 0.5px; text-transform: uppercase; margin-bottom: 6px; display: block; }
.profile-field .value { font-size: 0.9rem; color: var(--text); }
.profile-field input, .profile-field select, .profile-field textarea { width: 100%; padding: 9px 12px; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--radius-sm); color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 0.88rem; outline: none; transition: border-color 0.2s; }
.profile-field input:focus, .profile-field select:focus, .profile-field textarea:focus { border-color: var(--accent); }
.profile-field textarea { resize: vertical; min-height: 80px; }
.tags-display { display: flex; flex-wrap: wrap; gap: 6px; }
.profile-tag { padding: 4px 12px; border-radius: 20px; font-size: 0.78rem; background: var(--bg3); border: 1px solid var(--border); color: var(--text2); }
.profile-tag.removable { cursor: pointer; }
.profile-tag.removable:hover { background: rgba(255,77,106,0.1); border-color: var(--danger); color: var(--danger); }
.tag-input-wrap { display: flex; gap: 8px; margin-top: 8px; }
.tag-add-btn { padding: 8px 14px; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--radius-sm); color: var(--text2); cursor: pointer; font-size: 0.82rem; font-family: 'DM Sans', sans-serif; transition: all 0.2s; white-space: nowrap; }
.tag-add-btn:hover { border-color: var(--accent); color: var(--accent); }
.profile-save-row { display: flex; gap: 10px; padding-top: 16px; }
.save-btn { padding: 10px 20px; background: linear-gradient(135deg, var(--accent), var(--accent2)); border: none; border-radius: var(--radius-sm); color: #fff; font-family: 'DM Sans', sans-serif; font-size: 0.9rem; font-weight: 600; cursor: pointer; }
.cancel-btn { padding: 10px 20px; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--radius-sm); color: var(--text2); font-family: 'DM Sans', sans-serif; font-size: 0.9rem; cursor: pointer; }
.cancel-btn:hover { border-color: var(--danger); color: var(--danger); }

/* EMPTY STATE */
.empty-state { text-align: center; padding: 48px 24px; color: var(--text3); }
.empty-state .empty-icon { font-size: 2.5rem; margin-bottom: 12px; }
.empty-state p { font-size: 0.9rem; line-height: 1.6; }

@media (min-width: 600px) {
  .room-list { display: grid; grid-template-columns: 1fr 1fr; }
  .connect-grid { display: grid; grid-template-columns: 1fr 1fr; }
}
</style>
</head>
<body>

<!-- AUTH MODAL -->
<div id="auth-modal" class="modal-overlay hidden">
  <div class="modal-box">
    <div class="modal-head">
      <h2 id="auth-modal-title">Sign In</h2>
      <button class="modal-close" id="auth-modal-close">&times;</button>
    </div>
    <div class="modal-body">
      <!-- Sign In Form -->
      <div id="login-form">
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="login-email" placeholder="your@email.com">
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="login-password" placeholder="Enter your password">
        </div>
        <div id="login-error" class="form-error hidden"></div>
        <button class="auth-btn" id="login-submit-btn">Sign In</button>
        <p class="auth-switch">Don't have an account? <a href="#" id="switch-to-signup">Sign Up</a></p>
      </div>
      <!-- Register Form -->
      <div id="register-form" class="hidden">
        <div class="form-group">
          <label>Name</label>
          <input type="text" id="reg-name" placeholder="Your name" maxlength="30">
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="reg-email" placeholder="your@email.com">
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="reg-password" placeholder="Min 6 characters">
        </div>
        <div class="form-group">
          <label>Native Language</label>
          <select id="reg-native">
            <option value="">Select native language</option>
            <option>English</option><option>Spanish</option><option>French</option>
            <option>German</option><option>Italian</option><option>Portuguese</option>
            <option>Chinese</option><option>Japanese</option><option>Korean</option>
            <option>Arabic</option><option>Russian</option><option>Other</option>
          </select>
        </div>
        <div class="form-group">
          <label>Language You're Learning</label>
          <select id="reg-learning">
            <option value="">Select learning language</option>
            <option>English</option><option>Spanish</option><option>French</option>
            <option>German</option><option>Italian</option><option>Portuguese</option>
            <option>Chinese</option><option>Japanese</option><option>Korean</option>
            <option>Arabic</option><option>Russian</option><option>Other</option>
          </select>
        </div>
        <div id="reg-error" class="form-error hidden"></div>
        <button class="auth-btn" id="reg-submit-btn">Create Account</button>
        <p class="auth-switch">Already have an account? <a href="#" id="switch-to-signin">Sign In</a></p>
      </div>
    </div>
  </div>
</div>

<!-- CREATE ROOM MODAL -->
<div id="create-room-modal" class="modal-overlay hidden">
  <div class="modal-box">
    <div class="modal-head">
      <h2>Create Talk Room</h2>
      <button class="modal-close" id="close-create-room">&times;</button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label>Room Name</label>
        <input type="text" id="cr-name" placeholder="e.g. English Practice" maxlength="40">
      </div>
      <div class="form-group">
        <label>Language</label>
        <select id="cr-lang">
          <option value="">Select language</option>
          <option>English</option><option>Spanish</option><option>French</option>
          <option>German</option><option>Japanese</option><option>Korean</option>
          <option>Chinese</option><option>Arabic</option><option>Italian</option>
          <option>Portuguese</option><option>Russian</option>
        </select>
      </div>
      <div class="form-group">
        <label>Topic (optional)</label>
        <input type="text" id="cr-topic" placeholder="e.g. Travel, Business, Casual" maxlength="40">
      </div>
      <div id="cr-error" class="form-error hidden"></div>
      <button class="auth-btn" id="cr-submit-btn">🎤 Create & Join Room</button>
    </div>
  </div>
</div>

<!-- CONNECT USER PANEL -->
<div id="connect-panel-overlay" class="connect-panel-overlay hidden">
  <div class="connect-panel">
    <div class="connect-panel-head">
      <div class="connect-panel-info">
        <h3 id="cp-name">User</h3>
        <p id="cp-info">Language partner</p>
      </div>
      <button class="modal-close" id="close-connect-panel">&times;</button>
    </div>
    <div class="connect-panel-meta" id="cp-meta"></div>
    <div id="cp-bio" style="font-size:.88rem;color:var(--text2);margin-bottom:14px;line-height:1.6;"></div>
    <div class="connect-actions-row">
      <button class="follow-btn" id="cp-follow-btn" style="flex:1">➕ Follow</button>
      <button class="msg-btn" id="cp-msg-btn" style="flex:1">💬 Message</button>
    </div>
    <div id="cp-chat-section" class="connect-chat hidden">
      <h4 style="margin-top:16px">Messages</h4>
      <div class="connect-msgs" id="cp-msgs"></div>
      <div class="chat-input-row">
        <input type="text" id="cp-msg-input" placeholder="Write a message...">
        <button class="chat-send-btn" id="cp-msg-send">Send</button>
      </div>
    </div>
  </div>
</div>

<!-- APP -->
<div id="phone-frame">
<div class="app" id="app">

  <!-- TOP BAR -->
  <div class="topbar" id="topbar">
    <span></span>
    <div class="topbar-user" id="topbar-auth-area">
      <button class="btn-sm btn-outline" id="topbar-signin">Sign In</button>
      <button class="btn-sm btn-primary" id="topbar-signup">Sign Up</button>
    </div>
    <div class="topbar-user hidden" id="topbar-user-area">
      <span class="topbar-name" id="topbar-username"></span>
      <button class="btn-sm btn-danger" id="topbar-logout">Logout</button>
    </div>
  </div>

  <!-- MAIN -->
  <div class="main" id="main-content">

    <!-- LANDING SCREEN -->
    <div id="screen-landing" class="screen active">
      <div class="landing-bg">
        <div class="landing-bg-blob blob1"></div>
        <div class="landing-bg-blob blob2"></div>
      </div>

      <!-- App Logo -->
      <div class="app-logo-wrap">
        <div class="app-logo-icon">
          <svg viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="16" cy="16" r="12" stroke="white" stroke-width="1.5" stroke-opacity="0.7"/>
            <ellipse cx="16" cy="16" rx="5" ry="12" stroke="white" stroke-width="1.5"/>
            <line x1="4" y1="16" x2="28" y2="16" stroke="white" stroke-width="1.5" stroke-opacity="0.7"/>
            <line x1="6" y1="10" x2="26" y2="10" stroke="white" stroke-width="1" stroke-opacity="0.45"/>
            <line x1="6" y1="22" x2="26" y2="22" stroke="white" stroke-width="1" stroke-opacity="0.45"/>
            <circle cx="22" cy="9" r="3.5" fill="#00d4a0" opacity="0.9"/>
            <text x="22" y="11.5" text-anchor="middle" font-size="4.5" fill="white" font-weight="bold">✓</text>
          </svg>
        </div>
        <div class="app-logo-text">
          <div class="app-logo-name">HiFiVE</div>
          <div class="app-logo-sub">Language Exchange</div>
        </div>
      </div>

      <!-- 3D Earth -->
      <div class="earth-container">
        <div class="earth-glow"></div>
        <div class="earth-ring"></div>
        <canvas id="earth-canvas"></canvas>
      </div>

      <h1>HiFiVE</h1>
      <p>Connect with language partners worldwide. Speak, chat, and grow together.</p>
      <div class="landing-perks">
        <div class="landing-perk"><div class="landing-perk-dot"></div><span>🎤 Live Talk Rooms</span></div>
        <div class="landing-perk"><div class="landing-perk-dot"></div><span>🔗 Connect with partners</span></div>
        <div class="landing-perk"><div class="landing-perk-dot"></div><span>🤚 HiFiVE motivation</span></div>
      </div>
    </div>

    <!-- TALK ROOMS SCREEN -->
    <div id="screen-talk" class="screen">
      <div id="room-list-view">
        <div class="section-header">
          <h2>🎤 Talk Rooms</h2>
          <p>Join a live room and start speaking</p>
        </div>
        <button class="create-room-btn" id="open-create-room">＋ Create a Room</button>
        <div class="room-list" id="room-cards"></div>
      </div>
      <div id="active-room-view" class="hidden">
        <div class="active-room">
          <div class="room-topbar">
            <button class="back-btn" id="leave-room-btn">← Leave</button>
            <div class="room-topbar-info">
              <h3 id="ar-name">Room</h3>
              <p id="ar-meta">Language · Topic</p>
            </div>
          </div>
          <div class="stage-area">
            <div class="stage-title">🎤 Stage (Speakers)</div>
            <div class="stage-avatars" id="stage-avatars"></div>
          </div>
          <div class="audience-area">
            <div class="stage-title">👥 Audience</div>
            <div class="audience-grid" id="audience-grid"></div>
            <button class="raise-hand-btn" id="raise-hand-btn">✋ Raise Hand</button>
          </div>
          <div class="chat-panel">
            <div class="stage-title">💬 Room Chat</div>
            <div class="chat-msgs" id="room-chat-msgs"></div>
            <div class="chat-input-row">
              <input type="text" id="room-chat-input" placeholder="Type a message...">
              <button class="emoji-btn2" id="record-btn">🎤</button>
              <div class="emoji-relative">
                <button class="emoji-btn2" id="room-emoji-btn">😊</button>
                <div class="emoji-picker-wrap hidden" id="room-emoji-picker">
                  <button class="emoji-pick">😊</button><button class="emoji-pick">😂</button>
                  <button class="emoji-pick">❤️</button><button class="emoji-pick">🔥</button>
                  <button class="emoji-pick">👍</button><button class="emoji-pick">🎉</button>
                  <button class="emoji-pick">✨</button><button class="emoji-pick">😍</button>
                  <button class="emoji-pick">🙏</button><button class="emoji-pick">💪</button>
                  <button class="emoji-pick">🌍</button><button class="emoji-pick">📚</button>
                </div>
              </div>
              <button class="chat-send-btn" id="room-chat-send">Send</button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- CONNECT SCREEN -->
    <div id="screen-connect" class="screen">
      <div class="section-header">
        <h2>🔗 Connect</h2>
        <p>Find language partners with similar interests</p>
      </div>
      <div class="connect-wrap">
        <div class="connect-grid" id="connect-cards"></div>
      </div>
    </div>

    <!-- HIFIVE SCREEN -->
    <div id="screen-hifive" class="screen">
      <div class="hifive-wrap">
        <div class="hifive-hero">
          <div style="font-size:2.5rem;margin-bottom:12px">🤚</div>
          <h3>Give a HiFiVE!</h3>
          <p>Celebrate language milestones by giving HiFiVEs to your partners. Every HiFiVE is a boost of motivation.</p>
          <button class="hifive-start-btn" id="give-hifive-btn">🤚 Give HiFiVE</button>
        </div>
        <div class="hifive-grid">
          <div class="hifive-stat-card"><div class="hifive-stat-num" id="stat-given">0</div><div class="hifive-stat-label">HiFiVEs Given</div></div>
          <div class="hifive-stat-card"><div class="hifive-stat-num" id="stat-received">0</div><div class="hifive-stat-label">HiFiVEs Received</div></div>
          <div class="hifive-stat-card"><div class="hifive-stat-num" id="stat-streak">0</div><div class="hifive-stat-label">Day Streak</div></div>
          <div class="hifive-stat-card"><div class="hifive-stat-num" id="stat-rank">#—</div><div class="hifive-stat-label">Community Rank</div></div>
        </div>
        <div class="leaderboard">
          <h3>🏆 Top HiFiVErs This Week</h3>
          <div id="lb-rows"></div>
        </div>
      </div>
    </div>

    <!-- PROFILE SCREEN -->
    <div id="screen-profile" class="screen">
      <div class="profile-wrap">
        <div class="profile-card">
          <div class="profile-card-header">
            <div class="profile-avatar-big" id="prof-avatar-btn">
              <span id="prof-avatar-emoji">👤</span>
              <img id="prof-avatar-img" src="" alt="" style="display:none">
              <div class="upload-overlay">📷</div>
            </div>
            <input type="file" id="avatar-file-input" accept="image/*" style="display:none">
            <div class="profile-main-info">
              <h3 id="prof-name-display">Your Name</h3>
              <div class="profile-status"><span class="status-dot"></span> Online</div>
              <div class="profile-langs" id="prof-langs-display"></div>
            </div>
            <button class="profile-edit-btn" id="prof-edit-btn">✏️ Edit</button>
          </div>
          <div class="profile-card-body" id="prof-view-body">
            <div class="profile-field"><label>Email</label><div class="value" id="pv-email">—</div></div>
            <div class="profile-field"><label>Location</label><div class="value" id="pv-location">—</div></div>
            <div class="profile-field"><label>Age</label><div class="value" id="pv-age">—</div></div>
            <div class="profile-field"><label>About Me</label><div class="value" id="pv-bio">—</div></div>
            <div class="profile-field"><label>Interests</label><div class="tags-display" id="pv-interests"></div></div>
            <div class="profile-field"><label>Hobbies</label><div class="tags-display" id="pv-hobbies"></div></div>
            <div class="profile-field"><label>Learning Goals</label><div class="tags-display" id="pv-goals"></div></div>
            <div class="profile-field"><label>Achievements</label><div class="tags-display" id="pv-achievements"></div></div>
          </div>
          <div class="profile-card-body hidden" id="prof-edit-body">
            <div class="profile-field"><label>Display Name</label><input type="text" id="pe-name" placeholder="Your name"></div>
            <div class="profile-field"><label>Location</label><input type="text" id="pe-location" placeholder="City, Country"></div>
            <div class="profile-field"><label>Age</label><input type="number" id="pe-age" placeholder="Your age" min="13" max="99"></div>
            <div class="profile-field"><label>Native Language</label>
              <select id="pe-native">
                <option>English</option><option>Spanish</option><option>French</option><option>German</option>
                <option>Japanese</option><option>Korean</option><option>Chinese</option><option>Arabic</option>
                <option>Portuguese</option><option>Russian</option><option>Italian</option><option>Other</option>
              </select>
            </div>
            <div class="profile-field"><label>Learning Language</label>
              <select id="pe-learning">
                <option>English</option><option>Spanish</option><option>French</option><option>German</option>
                <option>Japanese</option><option>Korean</option><option>Chinese</option><option>Arabic</option>
                <option>Portuguese</option><option>Russian</option><option>Italian</option><option>Other</option>
              </select>
            </div>
            <div class="profile-field"><label>About Me</label><textarea id="pe-bio" placeholder="Tell others about yourself..." maxlength="500"></textarea></div>
            <div class="profile-field">
              <label>Interests</label>
              <div class="tags-display" id="pe-interests-tags"></div>
              <div class="tag-input-wrap">
                <input type="text" id="pe-interests-input" placeholder="Add interest…">
                <button type="button" class="tag-add-btn" data-target="interests">Add</button>
              </div>
            </div>
            <div class="profile-field">
              <label>Hobbies</label>
              <div class="tags-display" id="pe-hobbies-tags"></div>
              <div class="tag-input-wrap">
                <input type="text" id="pe-hobbies-input" placeholder="Add hobby…">
                <button type="button" class="tag-add-btn" data-target="hobbies">Add</button>
              </div>
            </div>
            <div class="profile-field">
              <label>Learning Goals</label>
              <div class="tags-display" id="pe-goals-tags"></div>
              <div class="tag-input-wrap">
                <input type="text" id="pe-goals-input" placeholder="Add goal…">
                <button type="button" class="tag-add-btn" data-target="goals">Add</button>
              </div>
            </div>
            <div class="profile-field">
              <label>Achievements</label>
              <div class="tags-display" id="pe-achievements-tags"></div>
              <div class="tag-input-wrap">
                <input type="text" id="pe-achievements-input" placeholder="Add achievement…">
                <button type="button" class="tag-add-btn" data-target="achievements">Add</button>
              </div>
            </div>
            <div class="profile-save-row">
              <button class="save-btn" id="prof-save-btn">💾 Save</button>
              <button class="cancel-btn" id="prof-cancel-btn">Cancel</button>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div><!-- /main -->

  <!-- BOTTOM NAV — only visible after login -->
  <nav class="bottom-nav hidden" id="bottom-nav">
    <button class="nav-item active" data-screen="screen-talk" id="nav-talk">
      <span class="nav-icon">🎤</span><span>Talk</span>
    </button>
    <button class="nav-item" data-screen="screen-connect" id="nav-connect">
      <span class="nav-icon">🔗</span><span>Connect</span>
    </button>
    <button class="nav-item" data-screen="screen-hifive" id="nav-hifive">
      <span class="nav-icon">🤚</span><span>HiFiVE</span>
    </button>
    <button class="nav-item" data-screen="screen-profile" id="nav-me">
      <span class="nav-icon">👤</span><span>Me</span>
    </button>
  </nav>

</div><!-- /app -->
</div>

<script>
// ── STATE ┛
let currentUser = null;
let editTags = { interests: [], hobbies: [], goals: [], achievements: [] };
let currentRoom = null;
let openPanelUser = null;
let panelMessages = {};

// ── SAMPLE FALLBACK DATA ──
const SAMPLE_ROOMS_DEFAULT = [
  { id: 'sr1', name: 'English Conversation', language: 'English', topic: 'Casual Chat', createdBy: 'HiFiVE Team' },
  { id: 'sr2', name: 'Spanish Practice', language: 'Spanish', topic: 'Travel', createdBy: 'HiFiVE Team' },
  { id: 'sr3', name: 'Japanese Beginners', language: 'Japanese', topic: 'Anime & Culture', createdBy: 'HiFiVE Team' }
];
const SAMPLE_USERS = [
  { id: 'u1', name: 'Yuki', nativeLanguage: 'Japanese', learningLanguage: 'English', location: 'Tokyo', bio: 'I love anime and travel!', interests: ['Anime','Travel'], status: 'Online', emoji: '👩', hifivesReceived: 142 },
  { id: 'u2', name: 'Carlos', nativeLanguage: 'Spanish', learningLanguage: 'English', location: 'Mexico City', bio: 'Musician and language nerd.', interests: ['Music','Tech'], status: 'Online', emoji: '👨', hifivesReceived: 98 }
];
const BOT_MESSAGES = [
  'Hello everyone!',
  'How is everyone doing today?',
  'I love practicing languages!',
  'Anyone want to talk about travel?',
  'Great room, thanks for creating it!',
  'What\'s your favorite word in your native language?',
  'Let\'s share some culture!',
  'I\'m learning new words every day.',
  'Anyone from Tokyo?',
  'This is fun!',
  'How long have you been learning?',
  'I need to practice my pronunciation.',
  'What music do you like?',
  'Let\'s exchange tips!',
  'See you in the next room!',
];
const LB_DATA = [
  { name: 'Lena Schmidt', pts: 211 },
  { name: 'Sofia Rossi', pts: 183 },
  { name: 'Yuki Tanaka', pts: 142 },
  { name: 'Carlos Mendez', pts: 98 },
  { name: 'Ryo Nakamura', pts: 75 }
];

// ── AUTH & API HELPERS (localStorage-based, no backend needed) ──
const SESSION_KEY = 'hifive_session';
const USERS_KEY = 'hifive_users';
let authToken = null;
let socket = null;
let userRooms = [];

function getAllUsers() {
  try { return JSON.parse(localStorage.getItem(USERS_KEY) || '{}'); } catch { return {}; }
}
function saveAllUsers(users) {
  localStorage.setItem(USERS_KEY, JSON.stringify(users));
}

function $(id) { return document.getElementById(id); }
function showToast(message) {
  const toast = document.createElement('div');
  toast.className = 'toast';
  toast.textContent = message;
  document.body.appendChild(toast);
  setTimeout(() => toast.remove(), 2800);
}

function saveSession() {
  if (!currentUser) return;
  localStorage.setItem(SESSION_KEY, JSON.stringify({ token: authToken || '', user: currentUser }));
}

function loadSessionData() {
  try {
    return JSON.parse(localStorage.getItem(SESSION_KEY));
  } catch {
    return null;
  }
}

function clearSession() {
  localStorage.removeItem(SESSION_KEY);
  currentUser = null;
  authToken = null;
  if (socket) {
    socket.disconnect();
    socket = null;
  }
}

function loadSession() {
  return loadSessionData();
}

function normalizeUser(user) {
  if (!user) return null;
  return {
    ...user,
    name: user.name || user.username || (user.email ? user.email.split('@')[0] : 'Guest'),
    native: user.native || user.nativeLanguage || '',
    learning: user.learning || user.learningLanguage || '',
    interests: user.interests || [],
    hobbies: user.hobbies || [],
    goals: user.goals || [],
    achievements: user.achievements || [],
    bio: user.bio || '',
    location: user.location || '',
    age: user.age || '',
    avatarUrl: user.avatarUrl || user.profilePicture || ''
  };
}

function connectSocket() {
  if (window.io && !socket) {
    socket = io();
  }
}

function saveUser(user) {
  if (!user) return;
  localStorage.setItem('hifive_user', JSON.stringify(user));
}

function loadProfile(email) {
  const stored = JSON.parse(localStorage.getItem('hifive_profiles') || '[]');
  return stored.find(profile => profile.email === email) || null;
}

function saveProfile(profile) {
  if (!profile || !profile.email) return;
  const stored = JSON.parse(localStorage.getItem('hifive_profiles') || '[]');
  const index = stored.findIndex(item => item.email === profile.email);
  if (index >= 0) {
    stored[index] = profile;
  } else {
    stored.unshift(profile);
  }
  localStorage.setItem('hifive_profiles', JSON.stringify(stored));
  if (currentUser && currentUser.email === profile.email) {
    currentUser = profile;
  }
}

function loadUserRooms() {
  return JSON.parse(localStorage.getItem('hifive_rooms') || '[]');
}

function saveUserRooms(rooms) {
  localStorage.setItem('hifive_rooms', JSON.stringify(rooms || []));
}

async function apiRequest(path, method = 'GET', body = null, requireAuth = true) {
  const users = getAllUsers();

  if (path === '/auth/register' && method === 'POST') {
    const key = body.email.toLowerCase();
    if (users[key]) throw new Error('An account with this email already exists.');
    const user = normalizeUser({ ...body, username: body.username, email: body.email });
    users[key] = { password: body.password, profile: user };
    saveAllUsers(users);
    return { user, token: 'local_' + key };
  }

  if (path === '/auth/login' && method === 'POST') {
    const key = body.email.toLowerCase();
    const record = users[key];
    if (!record) throw new Error('No account found with that email.');
    if (record.password !== body.password) throw new Error('Incorrect password.');
    return { user: record.profile, token: 'local_' + key };
  }

  if (path === '/auth/profile' && method === 'GET') {
    if (!authToken) throw new Error('Not authenticated.');
    const key = authToken.replace('local_', '');
    const record = users[key];
    if (!record) throw new Error('User not found.');
    return { user: record.profile };
  }

  throw new Error('Unknown API path: ' + path);
}

function setSession(token, user) {
  authToken = token;
  currentUser = user;
  saveSession();
  updateAuthUI();
}

async function restoreSession() {
  const session = loadSessionData();
  if (!session || !session.token || !session.user) return false;
  authToken = session.token;
  currentUser = session.user;

  try {
    const response = await apiRequest('/auth/profile', 'GET', null, true);
    currentUser = response.user;
    saveSession();
    updateAuthUI();
    return true;
  } catch {
    clearSession();
    return false;
  }
}

// ── TOAST ──
function toast(msg) {
  const t = document.createElement('div');
  t.className = 'toast'; t.textContent = msg;
  document.body.appendChild(t);
  setTimeout(() => t.remove(), 2700);
}

// ── SHOW ERROR ──
function showError(id, msg) {
  const el = document.getElementById(id);
  el.textContent = msg; el.classList.remove('hidden');
}
function clearError(id) { document.getElementById(id).classList.add('hidden'); }

// ── SCREEN NAV ──
function showScreen(screenId) {
  document.querySelectorAll('.screen').forEach(screen => screen.classList.toggle('active', screen.id === screenId));
  document.querySelectorAll('.nav-item').forEach(nav => nav.classList.toggle('active', nav.dataset.screen === screenId));

}

// ── AUTH UI ──
function openAuth(mode) {
  document.getElementById('auth-modal').classList.remove('hidden');
  setAuthMode(mode);
}
function closeAuth() { document.getElementById('auth-modal').classList.add('hidden'); }
function setAuthMode(mode) {
  const isIn = mode === 'signin';
  document.getElementById('auth-modal-title').textContent = isIn ? 'Sign In' : 'Create Account';
  document.getElementById('login-form').classList.toggle('hidden', !isIn);
  document.getElementById('register-form').classList.toggle('hidden', isIn);
  clearError('login-error'); clearError('reg-error');
}

// ── SIGN IN ──
document.getElementById('login-submit-btn').onclick = async () => {
  const email = document.getElementById('login-email').value.trim();
  const pass = document.getElementById('login-password').value;
  clearError('login-error');
  if (!email || !pass) { showError('login-error', 'Please fill in all fields.'); return; }
  try {
    const data = await apiRequest('/auth/login', 'POST', { email, password: pass }, false);
    loginSuccess(data.user, data.token);
    toast('👋 Welcome back, ' + data.user.username + '!');
  } catch (error) {
    showError('login-error', error.message || 'Login failed.');
  }
};

// ── SIGN UP ──
document.getElementById('reg-submit-btn').onclick = async () => {
  const name = document.getElementById('reg-name').value.trim();
  const email = document.getElementById('reg-email').value.trim();
  const pass = document.getElementById('reg-password').value;
  const native = document.getElementById('reg-native').value;
  const learning = document.getElementById('reg-learning').value;
  clearError('reg-error');
  if (!name || !email || !pass || !native || !learning) { showError('reg-error', 'Please fill in all fields.'); return; }
  if (name.length < 2) { showError('reg-error', 'Name must be at least 2 characters.'); return; }
  if (!email.includes('@') || !email.includes('.')) { showError('reg-error', 'Please enter a valid email address.'); return; }
  if (pass.length < 6) { showError('reg-error', 'Password must be at least 6 characters.'); return; }
  if (native === learning) { showError('reg-error', 'Native and learning languages must be different.'); return; }

  try {
    const data = await apiRequest('/auth/register', 'POST', {
      username: name,
      email,
      password: pass,
      nativeLanguage: native,
      learningLanguage: learning
    }, false);
    loginSuccess(data.user, data.token);
    toast('🎉 Welcome to HiFiVE, ' + name + '!');
  } catch (error) {
    showError('reg-error', error.message || 'Registration failed.');
  }
};

function loginSuccess(profile, token = null) {
  currentUser = normalizeUser(profile);
  if (token) {
    setSession(token, currentUser);
  } else {
    saveSession();
  }
  saveProfile(currentUser);
  userRooms = loadUserRooms();
  closeAuth();
  updateAuthUI();
  showScreen('screen-talk');
  renderRooms();
  renderConnect();
  renderHiFiVE();
  renderProfileView();
}

function logout() {
  currentUser = null;
  localStorage.removeItem('hifive_session');
  if (chatInterval) { clearInterval(chatInterval); chatInterval = null; }
  currentRoom = null;
  document.getElementById('active-room-view').classList.add('hidden');
  document.getElementById('room-list-view').classList.remove('hidden');
  updateAuthUI();
  showScreen('screen-landing');
  toast('👋 Logged out. See you soon!');
}

function updateAuthUI() {
  const loggedIn = !!currentUser;
  document.getElementById('topbar-auth-area').classList.toggle('hidden', loggedIn);
  document.getElementById('topbar-user-area').classList.toggle('hidden', !loggedIn);
  document.getElementById('bottom-nav').classList.toggle('hidden', !loggedIn);
  if (loggedIn) document.getElementById('topbar-username').textContent = '👋 ' + currentUser.name;
}

// ── TOPBAR BUTTONS ──
document.getElementById('topbar-signin').onclick = () => openAuth('signin');
document.getElementById('topbar-signup').onclick = () => openAuth('signup');
document.getElementById('topbar-logout').onclick = logout;

document.getElementById('auth-modal-close').onclick = closeAuth;
document.getElementById('auth-modal').onclick = e => { if (e.target === document.getElementById('auth-modal')) closeAuth(); };
document.getElementById('switch-to-signup').onclick = e => { e.preventDefault(); setAuthMode('signup'); };
document.getElementById('switch-to-signin').onclick = e => { e.preventDefault(); setAuthMode('signin'); };

// Enter key on login
document.getElementById('login-password').addEventListener('keydown', e => { if (e.key === 'Enter') document.getElementById('login-submit-btn').click(); });
document.getElementById('login-email').addEventListener('keydown', e => { if (e.key === 'Enter') document.getElementById('login-submit-btn').click(); });

// ── BOTTOM NAV ──
document.querySelectorAll('.nav-item').forEach(btn => {
  btn.onclick = () => {
    if (!currentUser) { openAuth('signin'); return; }
    showScreen(btn.dataset.screen);
    if (btn.dataset.screen === 'screen-profile') renderProfileView();
    if (btn.dataset.screen === 'screen-talk') renderRooms();
    if (btn.dataset.screen === 'screen-connect') renderConnect();
    if (btn.dataset.screen === 'screen-hifive') renderHiFiVE();
  };
});

// ── ROOMS ──
function getAllRooms() {
  const stored = loadUserRooms();
  return [...stored, ...SAMPLE_ROOMS_DEFAULT];
}

function renderRooms() {
  const container = document.getElementById('room-cards');
  container.innerHTML = '';
  const allRooms = getAllRooms();
  allRooms.forEach(room => {
    const card = document.createElement('div');
    card.className = 'room-card';
    const speakerCount = room.speakers ? room.speakers.length : 1;
    const audienceCount = room.audience ? room.audience.length : 0;
    const speakerNames = room.speakers ? room.speakers.slice(0,2).join(', ') + (room.speakers.length > 2 ? '…' : '') : (room.createdBy || '');
    const createdByBadge = room.isUserRoom ? `<span class="tag tag-purple">Created by ${room.createdBy}</span>` : '';
    card.innerHTML = `
      <div class="room-card-left">
        <div class="room-card-name">${room.name}</div>
        <div class="room-card-meta">
          <span class="tag">${room.lang}</span>
          ${room.topic ? `<span class="tag tag-green">${room.topic}</span>` : ''}
          ${createdByBadge}
        </div>
        <div style="font-size:.8rem;color:var(--text3);margin-top:4px">${speakerNames}</div>
      </div>
      <div class="room-card-count">
        <div class="room-count-num">${speakerCount + audienceCount}</div>
        <div class="room-count-label">in room</div>
      </div>
    `;
    card.onclick = () => joinRoom(room);
    container.appendChild(card);
  });
}

function joinRoom(room) {
  currentRoom = room;
  document.getElementById('ar-name').textContent = room.name;
  document.getElementById('ar-meta').textContent = `${room.lang}${room.topic ? ' · ' + room.topic : ''}`;
  // Stage
  const stageEl = document.getElementById('stage-avatars');
  stageEl.innerHTML = '';
  const speakers = room.speakers && room.speakers.length > 0 ? [...room.speakers] : [];
  if (room.isUserRoom) speakers.unshift(room.createdBy + ' (Host)');
  const allSpeakers = [...speakers, currentUser.name + ' (You)'];
  allSpeakers.forEach(name => {
    const wrap = document.createElement('div');
    wrap.className = 'stage-avatar';
    const circle = document.createElement('div');
    const classes = ['avatar-circle'];
    if (Math.random() > 0.5) classes.push('speaking');
    if (Math.random() > 0.7) classes.push('muted');
    circle.className = classes.join(' ');
    circle.textContent = name[0].toUpperCase();
    const label = document.createElement('div');
    label.className = 'avatar-name';
    label.textContent = name.split(' ')[0];
    wrap.appendChild(circle); wrap.appendChild(label);
    stageEl.appendChild(wrap);
  });
  // Audience
  const audEl = document.getElementById('audience-grid');
  audEl.innerHTML = '';
  const audience = room.audience || [];
  audience.forEach(name => {
    const chip = document.createElement('div');
    chip.className = 'audience-chip';
    chip.innerHTML = `<span class="dot"></span>${name}`;
    audEl.appendChild(chip);
  });
  if (audience.length === 0) {
    audEl.innerHTML = '<span style="color:var(--text3);font-size:.85rem">No one in audience yet</span>';
  }
  // Chat seed
  const chatEl = document.getElementById('room-chat-msgs');
  chatEl.innerHTML = '';
  const firstSpeaker = (room.speakers && room.speakers[0]) ? room.speakers[0].split(' ')[0] : (room.createdBy || 'Host');
  addChatMsg(firstSpeaker, 'Welcome to ' + room.name + '! 🎉');
  if (room.speakers && room.speakers[1]) addChatMsg(room.speakers[1].split(' ')[0], 'Great to be here!');
  document.getElementById('room-list-view').classList.add('hidden');
  document.getElementById('active-room-view').classList.remove('hidden');
  // Auto-chat
  if (chatInterval) clearInterval(chatInterval);
  const botSpeakers = (room.speakers && room.speakers.length > 0) ? room.speakers : [firstSpeaker];
  chatInterval = setInterval(() => {
    const speaker = botSpeakers[Math.floor(Math.random() * botSpeakers.length)];
    addChatMsg(speaker.split(' ')[0], BOT_MESSAGES[Math.floor(Math.random() * BOT_MESSAGES.length)]);
  }, 4000 + Math.random() * 4000);
  toast('🎤 Joined ' + room.name);
}

function addChatMsg(name, text) {
  const el = document.getElementById('room-chat-msgs');
  const div = document.createElement('div');
  div.className = 'chat-msg';
  const now = new Date();
  div.innerHTML = `<div class="chat-msg-avatar">${name[0].toUpperCase()}</div><div class="chat-msg-body"><div class="chat-msg-name">${name}</div><div class="chat-msg-text">${text}</div><div class="chat-msg-time">${now.getHours()}:${String(now.getMinutes()).padStart(2,'0')}</div></div>`;
  el.appendChild(div);
  el.scrollTop = el.scrollHeight;
}

document.getElementById('leave-room-btn').onclick = () => {
  if (chatInterval) { clearInterval(chatInterval); chatInterval = null; }
  currentRoom = null;
  document.getElementById('active-room-view').classList.add('hidden');
  document.getElementById('room-list-view').classList.remove('hidden');
  toast('👋 Left the room');
};

document.getElementById('room-chat-send').onclick = sendRoomChat;
document.getElementById('room-chat-input').addEventListener('keydown', e => { if (e.key === 'Enter') sendRoomChat(); });
function sendRoomChat() {
  const input = document.getElementById('room-chat-input');
  const text = input.value.trim();
  if (!text) return;
  addChatMsg(currentUser.name, text);
  input.value = '';
}

document.getElementById('room-emoji-btn').onclick = e => {
  e.stopPropagation();
  document.getElementById('room-emoji-picker').classList.toggle('hidden');
};
document.querySelectorAll('#room-emoji-picker .emoji-pick').forEach(btn => {
  btn.onclick = () => {
    document.getElementById('room-chat-input').value += btn.textContent;
    document.getElementById('room-emoji-picker').classList.add('hidden');
    document.getElementById('room-chat-input').focus();
  };
});
document.addEventListener('click', () => document.getElementById('room-emoji-picker').classList.add('hidden'));

// ── VOICE RECORDING ──
let mediaRecorder = null;
let audioChunks = [];

document.getElementById('record-btn').onclick = toggleRecording;

function toggleRecording() {
  const btn = document.getElementById('record-btn');
  if (mediaRecorder && mediaRecorder.state === 'recording') {
    mediaRecorder.stop();
    btn.textContent = '🎤';
    toast('🎤 Recording stopped');
  } else {
    startRecording();
    btn.textContent = '⏹️';
    toast('🎤 Recording started...');
  }
}

async function startRecording() {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
    mediaRecorder = new MediaRecorder(stream);
    audioChunks = [];
    mediaRecorder.ondataavailable = event => {
      audioChunks.push(event.data);
    };
    mediaRecorder.onstop = () => {
      const audioBlob = new Blob(audioChunks, { type: 'audio/wav' });
      const audioUrl = URL.createObjectURL(audioBlob);
      addAudioMsg(currentUser.name, audioUrl);
      stream.getTracks().forEach(track => track.stop());
    };
    mediaRecorder.start();
  } catch (error) {
    toast('❌ Could not access microphone');
    console.error(error);
  }
}

function addAudioMsg(name, audioUrl) {
  const el = document.getElementById('room-chat-msgs');
  const div = document.createElement('div');
  div.className = 'chat-msg';
  const now = new Date();
  div.innerHTML = `<div class="chat-msg-avatar">${name[0].toUpperCase()}</div><div class="chat-msg-body"><div class="chat-msg-name">${name}</div><div class="chat-msg-text"><audio controls src="${audioUrl}" style="max-width:200px;"></audio></div><div class="chat-msg-time">${now.getHours()}:${String(now.getMinutes()).padStart(2,'0')}</div></div>`;
  el.appendChild(div);
  el.scrollTop = el.scrollHeight;
}

document.getElementById('raise-hand-btn').onclick = function() {
  const raised = this.classList.toggle('raised');
  this.textContent = raised ? '✋ Hand Raised' : '✋ Raise Hand';
  if (raised) toast('✋ Hand raised! Wait to be invited to speak.');
};

// ── CREATE ROOM ──
document.getElementById('open-create-room').onclick = () => {
  if (!currentUser) { openAuth('signin'); return; }
  document.getElementById('create-room-modal').classList.remove('hidden');
  document.getElementById('cr-name').value = '';
  document.getElementById('cr-lang').value = '';
  document.getElementById('cr-topic').value = '';
  clearError('cr-error');
};
document.getElementById('close-create-room').onclick = () => document.getElementById('create-room-modal').classList.add('hidden');
document.getElementById('create-room-modal').onclick = e => { if (e.target === document.getElementById('create-room-modal')) document.getElementById('create-room-modal').classList.add('hidden'); };

document.getElementById('cr-submit-btn').onclick = () => {
  const name = document.getElementById('cr-name').value.trim();
  const lang = document.getElementById('cr-lang').value;
  const topic = document.getElementById('cr-topic').value.trim();
  clearError('cr-error');
  if (!name) { showError('cr-error', 'Please enter a room name.'); return; }
  if (!lang) { showError('cr-error', 'Please select a language.'); return; }
  const newRoom = {
    id: 'ur_' + Date.now(),
    name, lang, topic: topic || 'Open',
    speakers: [], audience: [],
    isUserRoom: true,
    createdBy: currentUser.name,
    createdAt: new Date().toISOString()
  };
  const stored = loadUserRooms();
  stored.unshift(newRoom);
  saveUserRooms(stored);
  userRooms = stored;
  document.getElementById('create-room-modal').classList.add('hidden');
  renderRooms();
  toast('🎤 Room "' + name + '" created!');
  setTimeout(() => joinRoom(newRoom), 300);
};

// ── CONNECT ──
function renderConnect() {
  const container = document.getElementById('connect-cards');
  container.innerHTML = '';
  SAMPLE_USERS.forEach(user => {
    const card = document.createElement('div');
    card.className = 'connect-card';
    card.innerHTML = `
      <div class="connect-avatar">${user.emoji}</div>
      <div class="connect-info">
        <div class="connect-name">${user.name}</div>
        <div class="connect-meta">
          <span class="tag">${user.nativeLanguage}</span>
          <span class="tag tag-green">Learning ${user.learningLanguage}</span>
        </div>
        <div class="connect-status ${user.status === 'Away' ? 'away' : ''}">${user.status === 'Online' ? '🟢 Online' : user.status === 'Away' ? '🟡 Away' : '⚫ Offline'}</div>
      </div>
    `;
    card.onclick = () => openConnectPanel(user);
    container.appendChild(card);
  });
}

function openConnectPanel(user) {
  openPanelUser = user;
  document.getElementById('cp-name').textContent = user.name;
  document.getElementById('cp-info').textContent = `${user.nativeLanguage} → ${user.learningLanguage} · ${user.location}`;
  document.getElementById('cp-meta').innerHTML = `<span class="tag">${user.nativeLanguage}</span><span class="tag tag-green">Learning ${user.learningLanguage}</span>`;
  document.getElementById('cp-bio').textContent = user.bio;
  document.getElementById('cp-chat-section').classList.add('hidden');
  document.getElementById('cp-follow-btn').className = 'follow-btn';
  document.getElementById('cp-follow-btn').textContent = '➕ Follow';
  if (!panelMessages[user.id]) panelMessages[user.id] = [];
  renderPanelMessages(user.id);
  document.getElementById('connect-panel-overlay').classList.remove('hidden');
}

function renderPanelMessages(uid) {
  const el = document.getElementById('cp-msgs');
  el.innerHTML = '';
  (panelMessages[uid] || []).forEach(msg => {
    const div = document.createElement('div');
    div.className = 'chat-msg';
    div.innerHTML = `<div class="chat-msg-avatar">${msg.from[0]}</div><div class="chat-msg-body"><div class="chat-msg-name">${msg.from}</div><div class="chat-msg-text">${msg.text}</div></div>`;
    el.appendChild(div);
  });
  el.scrollTop = el.scrollHeight;
}

document.getElementById('cp-follow-btn').onclick = function() {
  const following = this.classList.toggle('following');
  this.textContent = following ? '✅ Following' : '➕ Follow';
  if (following) toast('✅ Following ' + (openPanelUser?.name || ''));
};

document.getElementById('cp-msg-btn').onclick = () => {
  document.getElementById('cp-chat-section').classList.toggle('hidden');
  document.getElementById('cp-msg-input').focus();
};

document.getElementById('cp-msg-send').onclick = sendPanelMsg;
document.getElementById('cp-msg-input').addEventListener('keydown', e => { if (e.key === 'Enter') sendPanelMsg(); });
function sendPanelMsg() {
  const input = document.getElementById('cp-msg-input');
  const text = input.value.trim();
  if (!text || !openPanelUser) return;
  if (!panelMessages[openPanelUser.id]) panelMessages[openPanelUser.id] = [];
  panelMessages[openPanelUser.id].push({ from: currentUser.name, text });
  input.value = '';
  renderPanelMessages(openPanelUser.id);
  const replies = ['That\'s awesome!','Great! Let\'s practice sometime 😊','I totally agree!','When are you free to chat?','Cool! I\'m learning that too!'];
  setTimeout(() => {
    panelMessages[openPanelUser.id].push({ from: openPanelUser.name, text: replies[Math.floor(Math.random()*replies.length)] });
    renderPanelMessages(openPanelUser.id);
  }, 1200 + Math.random()*1500);
}

document.getElementById('close-connect-panel').onclick = () => document.getElementById('connect-panel-overlay').classList.add('hidden');
document.getElementById('connect-panel-overlay').onclick = e => { if (e.target === document.getElementById('connect-panel-overlay')) document.getElementById('connect-panel-overlay').classList.add('hidden'); };

// ── HIFIVE ──
function renderHiFiVE() {
  if (!currentUser) return;
  document.getElementById('stat-given').textContent = currentUser.hifivesGiven || 0;
  document.getElementById('stat-received').textContent = currentUser.hifivesReceived || 0;
  document.getElementById('stat-streak').textContent = currentUser.streak || 1;
  const sorted = [...LB_DATA].sort((a, b) => b.pts - a.pts);
  document.getElementById('stat-rank').textContent = '#' + (sorted.length + 1);
  const lbEl = document.getElementById('lb-rows');
  lbEl.innerHTML = '';
  const rankClass = ['gold','silver','bronze'];
  sorted.forEach((row, i) => {
    const div = document.createElement('div');
    div.className = 'lb-row';
    div.innerHTML = `<div class="lb-rank ${rankClass[i]||''}">${i===0?'🥇':i===1?'🥈':i===2?'🥉':i+1}</div><div class="lb-name">${row.name}</div><div class="lb-pts">${row.pts} 🤚</div>`;
    lbEl.appendChild(div);
  });
}

document.getElementById('give-hifive-btn').onclick = () => {
  if (!currentUser) { openAuth('signin'); return; }
  const target = SAMPLE_USERS[Math.floor(Math.random()*SAMPLE_USERS.length)];
  currentUser.hifivesGiven = (currentUser.hifivesGiven || 0) + 1;
  saveProfile(currentUser);
  renderHiFiVE();
  const btn = document.getElementById('give-hifive-btn');
  btn.textContent = '🎉 HiFiVE Sent!';
  btn.style.background = 'linear-gradient(135deg, #00d4a0, #00b894)';
  setTimeout(() => { btn.textContent = '🤚 Give HiFiVE'; btn.style.background = ''; }, 1800);
  toast('🤚 HiFiVE given to ' + target.name + '!');
};

// ── PROFILE ──
function renderProfileView() {
  if (!currentUser) return;
  const p = currentUser;
  document.getElementById('prof-name-display').textContent = p.name;
  document.getElementById('topbar-username').textContent = '👋 ' + p.name;
  const langsEl = document.getElementById('prof-langs-display');
  langsEl.innerHTML = `<span class="tag">${p.native}</span><span class="tag tag-green">Learning ${p.learning}</span>`;
  document.getElementById('pv-email').textContent = p.email || '—';
  document.getElementById('pv-location').textContent = p.location || '—';
  document.getElementById('pv-age').textContent = p.age || '—';
  document.getElementById('pv-bio').textContent = p.bio || '—';
  renderTagsView('pv-interests', p.interests);
  renderTagsView('pv-hobbies', p.hobbies);
  renderTagsView('pv-goals', p.goals);
  renderTagsView('pv-achievements', p.achievements);
  if (p.avatarUrl) {
    document.getElementById('prof-avatar-img').src = p.avatarUrl;
    document.getElementById('prof-avatar-img').style.display = 'block';
    document.getElementById('prof-avatar-emoji').style.display = 'none';
  } else {
    document.getElementById('prof-avatar-img').style.display = 'none';
    document.getElementById('prof-avatar-emoji').style.display = '';
  }
}

function renderTagsView(containerId, tags) {
  const el = document.getElementById(containerId);
  el.innerHTML = '';
  if (!tags || !tags.length) { el.innerHTML = '<span style="color:var(--text3);font-style:italic;font-size:.85rem">None added</span>'; return; }
  tags.forEach(tag => { const span = document.createElement('span'); span.className = 'profile-tag'; span.textContent = tag; el.appendChild(span); });
}

function openEditMode() {
  const p = currentUser;
  document.getElementById('pe-name').value = p.name || '';
  document.getElementById('pe-location').value = p.location || '';
  document.getElementById('pe-age').value = p.age || '';
  document.getElementById('pe-bio').value = p.bio || '';
  ['pe-native','pe-learning'].forEach((id, i) => {
    const sel = document.getElementById(id);
    const val = i === 0 ? p.native : p.learning;
    for (let o of sel.options) { o.selected = (o.value === val); }
  });
  editTags.interests = [...(p.interests || [])];
  editTags.hobbies = [...(p.hobbies || [])];
  editTags.goals = [...(p.goals || [])];
  editTags.achievements = [...(p.achievements || [])];
  renderEditTags();
  document.getElementById('prof-view-body').classList.add('hidden');
  document.getElementById('prof-edit-body').classList.remove('hidden');
}

function renderEditTags() {
  ['interests','hobbies','goals','achievements'].forEach(key => {
    const el = document.getElementById('pe-' + key + '-tags');
    el.innerHTML = '';
    editTags[key].forEach((tag, i) => {
      const span = document.createElement('span');
      span.className = 'profile-tag removable';
      span.textContent = tag + ' ✕';
      span.onclick = () => { editTags[key].splice(i, 1); renderEditTags(); };
      el.appendChild(span);
    });
  });
}

document.querySelectorAll('.tag-add-btn').forEach(btn => {
  btn.onclick = () => {
    const key = btn.dataset.target;
    const input = document.getElementById('pe-' + key + '-input');
    const val = input.value.trim();
    if (!val) return;
    if (!editTags[key].includes(val)) { editTags[key].push(val); renderEditTags(); }
    input.value = '';
  };
});
['interests','hobbies','goals','achievements'].forEach(key => {
  document.getElementById('pe-' + key + '-input').addEventListener('keydown', e => {
    if (e.key === 'Enter') { e.preventDefault(); document.querySelector(`.tag-add-btn[data-target="${key}"]`).click(); }
  });
});

document.getElementById('prof-edit-btn').onclick = () => { if (currentUser) openEditMode(); };
document.getElementById('prof-cancel-btn').onclick = () => {
  document.getElementById('prof-view-body').classList.remove('hidden');
  document.getElementById('prof-edit-body').classList.add('hidden');
};
document.getElementById('prof-save-btn').onclick = () => {
  currentUser.name = document.getElementById('pe-name').value.trim() || currentUser.name;
  currentUser.location = document.getElementById('pe-location').value.trim();
  currentUser.age = document.getElementById('pe-age').value.trim();
  currentUser.bio = document.getElementById('pe-bio').value.trim();
  currentUser.native = document.getElementById('pe-native').value;
  currentUser.learning = document.getElementById('pe-learning').value;
  currentUser.interests = [...editTags.interests];
  currentUser.hobbies = [...editTags.hobbies];
  currentUser.goals = [...editTags.goals];
  currentUser.achievements = [...editTags.achievements];
  saveProfile(currentUser);
  document.getElementById('prof-view-body').classList.remove('hidden');
  document.getElementById('prof-edit-body').classList.add('hidden');
  renderProfileView();
  toast('✅ Profile saved!');
};

// ── AVATAR ──
document.getElementById('prof-avatar-btn').onclick = () => {
  if (!document.getElementById('prof-edit-body').classList.contains('hidden')) document.getElementById('avatar-file-input').click();
};
document.getElementById('avatar-file-input').onchange = e => {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    currentUser.avatarUrl = ev.target.result;
    saveProfile(currentUser);
    document.getElementById('prof-avatar-img').src = ev.target.result;
    document.getElementById('prof-avatar-img').style.display = 'block';
    document.getElementById('prof-avatar-emoji').style.display = 'none';
    toast('📷 Avatar updated!');
  };
  reader.readAsDataURL(file);
};

// ── INIT ──
(async function init() {
  const restored = await restoreSession();
  if (restored) {
    userRooms = loadUserRooms();
    renderRooms();
    renderConnect();
    renderHiFiVE();
    renderProfileView();
    showScreen('screen-talk');
    return;
  }
  showScreen('screen-landing');
})();

// ── 3D EARTH ──
(function initEarth() {
  const canvas = document.getElementById('earth-canvas');
  if (!canvas) return;

  const W = 190, H = 190;
  canvas.width = W * 2;
  canvas.height = H * 2;
  canvas.style.width = W + 'px';
  canvas.style.height = H + 'px';

  const ctx = canvas.getContext('2d');
  const cx = canvas.width / 2, cy = canvas.height / 2;
  const R = canvas.width / 2 - 4;

  // Earth texture image
  const img = new Image();
  img.crossOrigin = 'anonymous';
  img.src = 'https://cdn.pixabay.com/objects3d/2026/03/25/04-56-04-904/render_720_720_0_340_0.png';

  let angle = 0;
  let textureLoaded = false;

  // Off-screen canvas to hold texture
  const texCanvas = document.createElement('canvas');
  const texW = 720, texH = 720;
  texCanvas.width = texW;
  texCanvas.height = texH;
  const texCtx = texCanvas.getContext('2d');

  img.onload = function() {
    texCtx.drawImage(img, 0, 0, texW, texH);
    textureLoaded = true;
  };

  img.onerror = function() {
    // Draw procedural earth if image fails
    textureLoaded = 'fallback';
  };

  function drawEarth(rot) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Clip to circle
    ctx.save();
    ctx.beginPath();
    ctx.arc(cx, cy, R, 0, Math.PI * 2);
    ctx.clip();

    if (textureLoaded === true) {
      // Sphere mapping: sample horizontal strip of texture
      // Map each pixel column to texture x based on rotation
      const texOffset = ((rot / (Math.PI * 2)) * texW) % texW;

      // Draw texture with spherical distortion
      for (let x = -R; x <= R; x++) {
        const nx = x / R; // normalized -1..1
        const cosLat = Math.sqrt(1 - nx * nx);
        const stripH = cosLat * R * 2;
        const stripY = cy - stripH / 2;

        // Longitude based on x position + rotation
        const lon = (Math.asin(nx) / Math.PI + 0.5 + rot / (Math.PI * 2));
        const texX = ((lon % 1 + 1) % 1) * texW;

        ctx.drawImage(
          texCanvas,
          texX, 0, 1, texH,
          cx + x, stripY, 1, stripH
        );
      }
    } else {
      // Fallback procedural earth
      const seaGrad = ctx.createRadialGradient(cx - R*0.2, cy - R*0.2, R*0.1, cx, cy, R);
      seaGrad.addColorStop(0, '#1a6bb5');
      seaGrad.addColorStop(0.6, '#0d4a8a');
      seaGrad.addColorStop(1, '#071e3d');
      ctx.fillStyle = seaGrad;
      ctx.fillRect(cx - R, cy - R, R*2, R*2);

      // Draw simple land masses
      ctx.fillStyle = '#2d8a4e';
      const lands = [
        [-0.35, -0.35, 0.32, 0.5],
        [0.1, -0.25, 0.22, 0.4],
        [-0.1, 0.15, 0.18, 0.25],
        [0.3, 0.1, 0.25, 0.3],
        [-0.45, 0.2, 0.2, 0.22],
      ];
      lands.forEach(([lx, ly, lw, lh]) => {
        ctx.beginPath();
        ctx.ellipse(cx + lx*R, cy + ly*R, lw*R, lh*R, rot*0.3, 0, Math.PI*2);
        ctx.fill();
      });
    }

    // Atmosphere haze
    const atmo = ctx.createRadialGradient(cx, cy, R * 0.75, cx, cy, R);
    atmo.addColorStop(0, 'rgba(0,80,200,0)');
    atmo.addColorStop(0.7, 'rgba(30,120,255,0.05)');
    atmo.addColorStop(1, 'rgba(80,160,255,0.35)');
    ctx.fillStyle = atmo;
    ctx.fillRect(cx - R - 2, cy - R - 2, (R + 2) * 2, (R + 2) * 2);

    // Specular highlight
    const spec = ctx.createRadialGradient(cx - R*0.35, cy - R*0.35, 0, cx - R*0.2, cy - R*0.2, R * 0.65);
    spec.addColorStop(0, 'rgba(255,255,255,0.22)');
    spec.addColorStop(0.4, 'rgba(255,255,255,0.06)');
    spec.addColorStop(1, 'rgba(0,0,0,0)');
    ctx.fillStyle = spec;
    ctx.fillRect(cx - R, cy - R, R*2, R*2);

    // Night shadow
    const shadow = ctx.createRadialGradient(cx + R*0.5, cy, R*0.3, cx + R*0.6, cy, R);
    shadow.addColorStop(0, 'rgba(0,0,0,0)');
    shadow.addColorStop(0.6, 'rgba(0,0,10,0.35)');
    shadow.addColorStop(1, 'rgba(0,0,20,0.75)');
    ctx.fillStyle = shadow;
    ctx.fillRect(cx - R, cy - R, R*2, R*2);

    ctx.restore();

    // Outer glow ring
    ctx.save();
    const outerGlow = ctx.createRadialGradient(cx, cy, R - 2, cx, cy, R + 8);
    outerGlow.addColorStop(0, 'rgba(74,144,226,0.3)');
    outerGlow.addColorStop(1, 'rgba(74,144,226,0)');
    ctx.fillStyle = outerGlow;
    ctx.beginPath();
    ctx.arc(cx, cy, R + 8, 0, Math.PI * 2);
    ctx.arc(cx, cy, R - 2, 0, Math.PI * 2, true);
    ctx.fill();
    ctx.restore();
  }

  let animId;
  function animate() {
    angle += 0.004;
    drawEarth(angle);
    animId = requestAnimationFrame(animate);
  }

  // Start immediately with fallback, update when image loads
  animate();

  // Pause animation when landing screen not visible to save resources
  const observer = new MutationObserver(() => {
    const landing = document.getElementById('screen-landing');
    if (landing && landing.classList.contains('active')) {
      if (!animId) animate();
    } else {
      if (animId) { cancelAnimationFrame(animId); animId = null; }
    }
  });
  const main = document.getElementById('main-content');
  if (main) observer.observe(main, { childList: true, subtree: true, attributes: true });
})();
</script>

</body>
</html>
