[index.html](https://github.com/user-attachments/files/34854040/index.html)
<!DOCTYPE html>
<html lang="zh-CN" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>CC 图库管理 · 本地媒体库</title>
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' rx='8' fill='%230A0B0D'/%3E%3Crect x='7' y='9' width='18' height='14' rx='3' fill='none' stroke='%23EDEFF2' stroke-width='1.6'/%3E%3Ccircle cx='12.5' cy='14' r='2' fill='%235C9BFF'/%3E%3Cpath d='M8.5 21.5l5-5.5 3.5 3.5 3-2.5 4 4.5' fill='none' stroke='%23EDEFF2' stroke-width='1.6'/%3E%3C/svg%3E">
<style>
/* ============ 基础 token ============ */
:root{
  --side-w:244px;
  --r-sm:4px; --r-md:8px; --r-lg:14px;
  --ease:cubic-bezier(.2,.7,.2,1);
  --font:"Segoe UI Variable Text","Segoe UI","PingFang SC","Microsoft YaHei UI","Microsoft YaHei",system-ui,sans-serif;
  --mono:"Cascadia Mono","SF Mono",ui-monospace,Consolas,monospace;
}
html[data-theme="dark"]{
  --bg:#08090B; --bg-2:#0C0E11; --panel:#0B0C0F; --elev:#12151A;
  --line:rgba(255,255,255,.075); --line-2:rgba(255,255,255,.14);
  --text:#ECEEF1; --text-2:#98A0AA; --text-3:#5C636D;
  --hover:rgba(255,255,255,.045); --active:rgba(255,255,255,.09);
  --accent:#5C9BFF; --accent-ink:#0A0C10;
  --btn-bg:#EDEFF2; --btn-ink:#08090B;
  --tile:#101318; --shadow:0 24px 60px rgba(0,0,0,.55);
  --scrim:rgba(4,5,7,.72);
  --glass:rgba(14,17,22,.56); --glass-2:rgba(19,23,29,.72);
  --glass-line:rgba(255,255,255,.10); --glass-hi:rgba(255,255,255,.075);
  --blob-a:rgba(64,124,224,.34); --blob-b:rgba(30,62,116,.38); --blob-c:rgba(255,255,255,.05);
}
html[data-theme="light"]{
  --bg:#FFFFFF; --bg-2:#F6F7F9; --panel:#FFFFFF; --elev:#FFFFFF;
  --line:rgba(9,11,14,.10); --line-2:rgba(9,11,14,.20);
  --text:#0A0C0F; --text-2:#555C66; --text-3:#9097A0;
  --hover:rgba(9,11,14,.04); --active:rgba(9,11,14,.075);
  --accent:#2563EB; --accent-ink:#FFFFFF;
  --btn-bg:#0A0C0F; --btn-ink:#FFFFFF;
  --tile:#F1F3F5; --shadow:0 24px 60px rgba(9,11,14,.16);
  --scrim:rgba(245,246,248,.80);
  --glass:rgba(255,255,255,.66); --glass-2:rgba(255,255,255,.84);
  --glass-line:rgba(9,11,14,.08); --glass-hi:rgba(255,255,255,.95);
  --blob-a:rgba(37,99,235,.13); --blob-b:rgba(148,163,184,.18); --blob-c:rgba(255,255,255,.6);
}
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%}
body{
  font-family:var(--font); background:var(--bg); color:var(--text);
  font-size:14px; line-height:1.55; overflow:hidden;
  -webkit-font-smoothing:antialiased; text-rendering:optimizeLegibility;
}
button,input,select,textarea{font:inherit;color:inherit;background:none;border:none;outline:none}
button{cursor:pointer}
svg{display:block}
::selection{background:var(--accent);color:#fff}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
.mono{font-family:var(--mono);font-variant-numeric:tabular-nums;letter-spacing:-.01em}
.hairline{background:var(--line)}

/* ============ 液态玻璃 ============ */
.bg{position:fixed;inset:0;z-index:0;overflow:hidden;background:var(--bg);pointer-events:none}
.bg i{position:absolute;display:block;border-radius:50%;filter:blur(72px);will-change:transform}
.bg .b1{width:56vw;height:56vw;left:-14vw;top:-22vw;background:radial-gradient(circle,var(--blob-a) 0%,transparent 68%);animation:floatA 24s ease-in-out infinite alternate}
.bg .b2{width:48vw;height:48vw;right:-12vw;top:6vh;background:radial-gradient(circle,var(--blob-b) 0%,transparent 66%);animation:floatB 30s ease-in-out infinite alternate}
.bg .b3{width:40vw;height:40vw;left:22vw;bottom:-18vw;background:radial-gradient(circle,var(--blob-c) 0%,transparent 70%);animation:floatA 34s ease-in-out infinite alternate-reverse}
@keyframes floatA{from{transform:translate3d(0,0,0) scale(1)}to{transform:translate3d(4vw,5vh,0) scale(1.12)}}
@keyframes floatB{from{transform:translate3d(0,0,0) scale(1.05)}to{transform:translate3d(-5vw,6vh,0) scale(.94)}}

/* 玻璃面板：同一套材质，靠背景光晕产生折射感 */
.sidebar,.topbar,.drawer,.modal-card,.pop,.toast,.selbar,.viewer-top,.viewer-bot{
  backdrop-filter:blur(22px) saturate(150%);
  -webkit-backdrop-filter:blur(22px) saturate(150%);
}
.sidebar{background:var(--glass);border-right:1px solid var(--glass-line);box-shadow:inset 0 1px 0 var(--glass-hi)}
.topbar{background:var(--glass);border-bottom:1px solid var(--glass-line);box-shadow:inset 0 1px 0 var(--glass-hi)}
.drawer{background:var(--glass-2);border-left:1px solid var(--glass-line)}
.modal-card{position:relative;background:var(--glass-2);border:1px solid var(--glass-line);box-shadow:var(--shadow),inset 0 1px 0 var(--glass-hi);animation:liquidPop .34s cubic-bezier(.18,1.3,.34,1)}
.pop{background:var(--glass-2);border:1px solid var(--glass-line)}
.toast{background:var(--glass-2);border:1px solid var(--glass-line);box-shadow:0 16px 38px rgba(0,0,0,.3),inset 0 1px 0 var(--glass-hi)}
.selbar{background:var(--glass-2);border:1px solid var(--glass-line);box-shadow:0 18px 40px rgba(0,0,0,.28),inset 0 1px 0 var(--glass-hi)}

/* 跟随指针的镜面高光（液态反光） */
.sidebar,.topbar,.drawer,.modal-card,.pop,.toast,.selbar{position:relative;isolation:isolate}
.sidebar::before,.topbar::before,.drawer::before,.modal-card::before,.pop::before,.toast::before,.selbar::before{
  content:"";position:absolute;inset:0;pointer-events:none;z-index:0;border-radius:inherit;
  background:radial-gradient(240px circle at var(--gx,50%) var(--gy,0%),rgba(255,255,255,.10),rgba(255,255,255,.03) 42%,transparent 70%);
  opacity:var(--gs,0);transition:opacity .4s var(--ease);
}
.sidebar > *,.topbar > *,.drawer > *,.modal-card > *,.pop > *,.toast > *,.selbar > *{position:relative;z-index:1}

/* 弹性 */
.modal-card{animation:liquidPop .34s cubic-bezier(.18,1.3,.34,1)}
@keyframes liquidPop{0%{opacity:0;transform:translateY(12px) scale(.94)}62%{opacity:1;transform:translateY(-1px) scale(1.006)}100%{opacity:1;transform:none}}
.drawer{transition:transform .46s cubic-bezier(.22,1,.36,1)}
.drawer.on .drawer-body{animation:drawerRise .5s cubic-bezier(.2,1,.3,1) .05s both}
.drawer.on .preview{animation:previewIn .46s cubic-bezier(.2,1,.3,1) both}
@keyframes drawerRise{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
@keyframes previewIn{from{opacity:0;transform:scale(.97)}to{opacity:1;transform:none}}
.btn:active,.chip:active,.tool:active,.nav-item:active{transform:scale(.975)}
.btn,.chip,.tool,.nav-item{transition:transform .14s var(--ease),background-color .18s var(--ease),color .18s var(--ease),border-color .18s var(--ease)}
@media (prefers-reduced-motion: reduce){
  .bg i{animation:none}
  .drawer,.drawer.on .drawer-body,.drawer.on .preview,.modal-card{animation:none;transition:transform .2s linear}
}

/* 滚动条 */
*::-webkit-scrollbar{width:10px;height:10px}
*::-webkit-scrollbar-thumb{background:var(--line-2);border:3px solid var(--bg);border-radius:8px}
*::-webkit-scrollbar-track{background:transparent}

/* ============ 布局骨架 ============ */
.app{display:grid;grid-template-columns:var(--side-w) 1fr;height:100vh;height:100dvh;overflow:hidden;position:relative;z-index:1}

/* ---------- 侧栏 ---------- */
.sidebar{
  display:flex;flex-direction:column;min-width:0;
  background:var(--bg-2);border-right:1px solid var(--line);
  transition:margin-left .32s var(--ease);
}
.brand{display:flex;align-items:center;gap:11px;padding:20px 18px 18px}
.brand-mark{
  width:34px;height:34px;border-radius:9px;flex:0 0 auto;position:relative;overflow:hidden;
  background:var(--btn-bg);display:grid;place-items:center;
}
.brand-mark svg{width:19px;height:19px;color:var(--btn-ink)}
.brand-name{display:flex;flex-direction:column;line-height:1.15;min-width:0}
.brand-name b{font-size:16px;font-weight:650;letter-spacing:.06em}
.brand-name span{font-size:10px;color:var(--text-3);letter-spacing:.18em;font-family:var(--mono)}

.nav{flex:1;overflow-y:auto;padding:6px 10px 10px}
.nav-group{margin-top:14px}
.nav-label{
  display:flex;align-items:center;justify-content:space-between;
  padding:0 8px 7px;font-size:11px;color:var(--text-3);letter-spacing:.04em;
}
.nav-item{
  display:flex;align-items:center;gap:10px;width:100%;height:36px;padding:0 10px;
  border-radius:var(--r-md);color:var(--text-2);text-align:left;position:relative;
  transition:background .16s,color .16s;
}
.nav-item:hover{background:var(--hover);color:var(--text)}
.nav-item .ico{width:17px;height:17px;flex:0 0 auto;color:var(--text-3);transition:color .16s}
.nav-item:hover .ico{color:var(--text-2)}
.nav-item .txt{flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:13px}
.nav-item .cnt{font-family:var(--mono);font-size:11px;color:var(--text-3)}
.nav-item[aria-current="true"]{background:var(--active);color:var(--text);font-weight:550}
.nav-item[aria-current="true"] .ico{color:var(--accent)}
.nav-item[aria-current="true"] .cnt{color:var(--text-2)}
.nav-item[aria-current="true"]::before{
  content:"";position:absolute;left:-10px;top:8px;bottom:8px;width:2px;background:var(--accent);border-radius:2px;
}
.nav-sub{display:flex;align-items:center;gap:8px;padding:0 8px 6px;font-size:11px;color:var(--text-3)}
.nav-sub .dot{width:6px;height:6px;border-radius:50%;background:var(--line-2);flex:0 0 auto}

.side-foot{border-top:1px solid var(--line);padding:12px 14px 14px;display:flex;flex-direction:column;gap:10px}
.storage{display:flex;flex-direction:column;gap:6px}
.storage-top{display:flex;justify-content:space-between;font-size:11px;color:var(--text-3)}
.storage-bar{height:3px;background:var(--line);border-radius:3px;overflow:hidden}
.storage-bar i{display:block;height:100%;background:var(--text);border-radius:3px;transition:width .5s var(--ease)}
.side-foot .note{font-size:11px;color:var(--text-3);line-height:1.5}
.side-meta{display:flex;align-items:center;gap:7px;font-family:var(--mono);font-size:10.5px;color:var(--text-3);letter-spacing:.02em}
.side-meta i{width:1px;height:9px;background:var(--line-2);display:block}

/* ---------- 主区 ---------- */
.main{display:flex;flex-direction:column;min-width:0;min-height:0;background:color-mix(in srgb,var(--bg) 88%,transparent);transition:margin-right .34s var(--ease)}
.app.withdrawer .main{margin-right:376px}

.topbar{
  flex:0 0 auto;height:60px;display:flex;align-items:center;gap:12px;
  padding:0 20px;border-bottom:1px solid var(--line);
  background:color-mix(in srgb,var(--bg) 82%,transparent);
  backdrop-filter:blur(14px);position:relative;z-index:6;
}
.crumb{display:flex;flex-direction:column;line-height:1.25;min-width:0;margin-right:auto}
.crumb h1{font-size:15px;font-weight:620;letter-spacing:.01em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.crumb p{font-size:11px;color:var(--text-3);font-family:var(--mono);margin-top:1px;white-space:nowrap}

.search{
  display:flex;align-items:center;gap:8px;width:250px;height:34px;padding:0 10px;
  border:1px solid var(--line);border-radius:var(--r-md);background:var(--panel);
  transition:border-color .18s,width .24s var(--ease);
}
.search:focus-within{border-color:var(--line-2);width:300px}
.search svg{width:15px;height:15px;color:var(--text-3);flex:0 0 auto}
.search input{flex:1;min-width:0;font-size:13px;background:none}
.search input::placeholder{color:var(--text-3)}
.search kbd{font-family:var(--mono);font-size:10px;color:var(--text-3);border:1px solid var(--line);border-radius:3px;padding:1px 4px}

.tool{width:34px;height:34px;display:grid;place-items:center;border-radius:var(--r-md);color:var(--text-2);transition:background .16s,color .16s}
.tool:hover{background:var(--hover);color:var(--text)}
.tool[aria-pressed="true"]{background:var(--active);color:var(--text)}
.tool svg{width:16px;height:16px}
.tool-div{width:1px;height:20px;background:var(--line)}

.btn{
  display:inline-flex;align-items:center;gap:7px;height:34px;padding:0 14px;border-radius:var(--r-md);
  background:var(--btn-bg);color:var(--btn-ink);font-size:13px;font-weight:600;
  transition:opacity .16s,transform .16s var(--ease);
}
.btn:hover{opacity:.86}
.btn:active{transform:scale(.98)}
.btn svg{width:15px;height:15px}
.btn.ghost{background:transparent;color:var(--text);border:1px solid var(--line-2);font-weight:500}
.btn.ghost:hover{background:var(--hover);opacity:1}
.btn.sm{height:30px;padding:0 11px;font-size:12px}

/* 筛选条 */
.subbar{
  flex:0 0 auto;display:flex;align-items:center;gap:8px;padding:9px 20px;
  border-bottom:1px solid var(--line);overflow-x:auto;scrollbar-width:thin;
}
.subbar::-webkit-scrollbar{height:0}
.chip{
  display:inline-flex;align-items:center;gap:6px;height:27px;padding:0 11px;border-radius:999px;
  font-size:12px;color:var(--text-2);border:1px solid transparent;background:var(--bg-2);
  white-space:nowrap;transition:.16s
}
.chip:hover{color:var(--text);background:var(--active)}
.chip[aria-pressed="true"]{background:var(--text);color:var(--bg);border-color:var(--text)}
.chip .n{font-family:var(--mono);font-size:10.5px;opacity:.65}
.subbar .spacer{flex:1}

/* ---------- 内容区 ---------- */
.content{flex:1;min-height:0;overflow-y:auto;overflow-x:hidden;position:relative;scroll-behavior:smooth}
.content-inner{padding:20px 20px 96px}

/* 空状态 */
.empty{
  min-height:calc(100vh - 200px);display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:40px 16px 80px;text-align:center;gap:0;
}
.empty-frame{
  width:min(720px,100%);aspect-ratio:21/9;border-radius:var(--r-lg);position:relative;
  display:grid;place-items:center;background:
    radial-gradient(circle at 50% 42%,color-mix(in srgb,var(--text) 5%,transparent),transparent 68%);
  transition:.2s;
}
.empty-frame::before{
  content:"";position:absolute;inset:0;border-radius:var(--r-lg);
  border:1px solid var(--line);
}
.empty-frame .corner{position:absolute;width:22px;height:22px;border:1px solid var(--text-3);opacity:.85}
.empty-frame .c1{top:-1px;left:-1px;border-right:none;border-bottom:none;border-top-left-radius:var(--r-lg)}
.empty-frame .c2{top:-1px;right:-1px;border-left:none;border-bottom:none;border-top-right-radius:var(--r-lg)}
.empty-frame .c3{bottom:-1px;left:-1px;border-right:none;border-top:none;border-bottom-left-radius:var(--r-lg)}
.empty-frame .c4{bottom:-1px;right:-1px;border-left:none;border-top:none;border-bottom-right-radius:var(--r-lg)}
.empty-frame.drag{border-color:var(--accent);background:color-mix(in srgb,var(--accent) 8%,transparent)}
.empty-frame .inner{display:flex;flex-direction:column;align-items:center;gap:14px;padding:24px}
.empty-ico{width:56px;height:56px;color:var(--text-3)}
.empty h2{font-size:22px;font-weight:600;letter-spacing:.02em}
.empty p{font-size:13px;color:var(--text-2);max-width:440px}
.empty-actions{display:flex;gap:10px;flex-wrap:wrap;justify-content:center;margin-top:6px}
.empty-tip{margin-top:22px;font-size:11.5px;color:var(--text-3);display:flex;gap:16px;flex-wrap:wrap;justify-content:center}
.empty-tip span{display:inline-flex;align-items:center;gap:5px}
.empty-tip b{font-family:var(--mono);color:var(--text-2);font-weight:500}

/* 照片网格 */
.grid{
  display:grid;grid-template-columns:repeat(var(--cols,5),minmax(0,1fr));gap:10px;
  align-content:start;
}
.grid.dense{gap:6px}
.tile{
  position:relative;border-radius:var(--r-md);overflow:hidden;background:var(--tile);cursor:pointer;
  aspect-ratio:1/1;border:1px solid var(--line);
  transition:transform .22s var(--ease),border-color .18s,box-shadow .22s;
  transform-origin:center;
}
.tile img{width:100%;height:100%;object-fit:cover;display:block;transition:transform .4s var(--ease),filter .3s}
.tile:hover{transform:translateY(-2px);border-color:var(--line-2);box-shadow:0 10px 26px rgba(0,0,0,.22)}
.tile:hover img{transform:scale(1.04)}
.tile.sel{border-color:var(--accent);box-shadow:0 0 0 1px var(--accent)}
.tile.sel img{filter:brightness(.82)}
.tile .badge{
  position:absolute;left:8px;top:8px;display:flex;gap:4px;z-index:2;
}.tile .cat{
  font-size:10.5px;line-height:1;padding:4px 6px;border-radius:4px;color:#fff;
  background:rgba(6,7,9,.62);backdrop-filter:blur(8px);font-weight:500;letter-spacing:.02em;
}
.tile .fav{position:absolute;right:8px;top:8px;width:20px;height:20px;display:grid;place-items:center;z-index:2}
.tile .fav svg{width:14px;height:14px;color:#fff;filter:drop-shadow(0 1px 3px rgba(0,0,0,.5))}
.tile .check{
  position:absolute;left:8px;top:8px;width:18px;height:18px;border-radius:50%;z-index:3;
  border:1.5px solid rgba(255,255,255,.8);display:none;place-items:center;background:rgba(6,7,9,.35)
}
.tile.sel .badge{display:none}
.tile.sel .check{display:grid;background:var(--accent);border-color:var(--accent)}
.tile .check svg{width:11px;height:11px;color:#fff}
.tile .meta{
  position:absolute;left:0;right:0;bottom:0;padding:22px 9px 7px;z-index:1;
  background:linear-gradient(to top,rgba(4,5,7,.78),rgba(4,5,7,.32) 55%,transparent);
  color:#fff;opacity:0;transform:translateY(4px);transition:.22s var(--ease);
}
.tile:hover .meta,.tile.sel .meta{opacity:1;transform:none}
.tile .meta b{display:block;font-size:11.5px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tile .meta span{font-size:10px;opacity:.62;font-family:var(--mono)}
.tile.sel .check{display:grid}
.tile.sel::after{content:"";position:absolute;inset:0;background:rgba(6,7,9,.25);z-index:0}

/* 加载 / 空筛选 */
.hollow{
  padding:80px 20px;text-align:center;color:var(--text-2);
  display:flex;flex-direction:column;align-items:center;gap:12px;
}
.hollow svg{width:40px;height:40px;color:var(--text-3)}
.hollow p{font-size:13px}
.hollow .btn{margin-top:2px}

/* 选择模式操作条 */
.selbar{
  position:absolute;left:50%;bottom:26px;transform:translate(-50%,16px);
  display:flex;align-items:center;gap:6px;padding:8px;border-radius:12px;
  width:max-content;max-width:calc(100vw - 32px);
  background:var(--elev);border:1px solid var(--line-2);box-shadow:var(--shadow);
  opacity:0;pointer-events:none;transition:.24s var(--ease);z-index:20;
  overflow-x:auto;scrollbar-width:none
}
.selbar::-webkit-scrollbar{height:0}
.selbar.on{opacity:1;transform:translate(-50%,0);pointer-events:auto}
.selbar .count{font-size:12px;color:var(--text-2);padding:0 8px;white-space:nowrap}
.selbar .count b{color:var(--text);font-family:var(--mono);font-weight:600}
.selbar button{
  display:inline-flex;align-items:center;gap:6px;height:30px;padding:0 10px;border-radius:7px;
  font-size:12px;color:var(--text-2);white-space:nowrap;flex:0 0 auto
}
.selbar button:hover{background:var(--hover);color:var(--text)}
.selbar button svg{width:14px;height:14px}
.selbar .danger:hover{color:#FF6B6B;background:rgba(255,107,107,.10)}
.selbar .vline{width:1px;height:18px;background:var(--line)}

/* ---------- 右侧详情面板 ---------- */
.drawer{
  position:fixed;top:0;right:0;bottom:0;width:376px;max-width:92vw;z-index:40;
  background:var(--panel);border-left:1px solid var(--line);
  transform:translateX(101%);transition:transform .34s var(--ease);
  display:flex;flex-direction:column;box-shadow:-24px 0 60px rgba(0,0,0,.18);
}
.drawer.on{transform:none}
.drawer-head{
  display:flex;align-items:center;gap:10px;padding:14px 14px 12px;border-bottom:1px solid var(--line);
}
.drawer-head h3{font-size:13px;font-weight:600;flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.drawer-head .tool{width:30px;height:30px}
.preview{
  background:
    linear-gradient(45deg,transparent 49%,var(--line) 49%,var(--line) 51%,transparent 51%),
    var(--bg-2);
  background-size:14px 14px;display:grid;place-items:center;padding:16px;
  flex:0 0 auto;min-height:220px;max-height:44vh;overflow:hidden;
}
.preview img{max-width:100%;max-height:calc(44vh - 32px);object-fit:contain;border-radius:2px;display:block}
.preview video{max-width:100%;max-height:calc(44vh - 32px);border-radius:2px;display:block;background:#000}
.preview .audio-box{width:100%;max-width:340px;display:flex;flex-direction:column;gap:10px;align-items:center}
.preview .audio-box .wave{width:100%;height:104px;border-radius:4px;background-size:contain;background-repeat:no-repeat;background-position:center;border:1px solid var(--line);background-color:#0c0e11}
.preview .audio-box audio{width:100%}
.tile .play{position:absolute;inset:0;display:grid;place-items:center;pointer-events:none;z-index:1}
.tile .play svg{width:32px;height:32px;color:#fff;opacity:.86;filter:drop-shadow(0 2px 8px rgba(0,0,0,.6))}
.viewer-stage video{max-width:100%;max-height:100%;object-fit:contain;background:#000;border-radius:2px}
.viewer-stage .vaudio{display:none;flex-direction:column;align-items:center;gap:18px;width:min(520px,80%)}
.viewer-stage .vaudio img{width:100%;max-height:46vh;object-fit:contain;border-radius:4px}
.viewer-stage .vaudio audio{width:100%}
.drawer-body{flex:1;overflow-y:auto;padding:16px 16px 90px}
.field{margin-bottom:18px}
.field > label{display:flex;align-items:center;justify-content:space-between;font-size:11px;color:var(--text-3);margin-bottom:7px;letter-spacing:.03em}
.field > label .mini{font-family:var(--mono);font-size:10px}
.cat-row{display:flex;flex-wrap:wrap;gap:6px}
.cat-row .chip{height:26px;padding:0 10px;font-size:11.5px}
.person-row{display:flex;flex-wrap:wrap;gap:6px;align-items:center}
.ptag{
  display:inline-flex;align-items:center;gap:5px;height:25px;padding:0 8px;border-radius:999px;
  background:var(--active);font-size:11.5px
}
.ptag button{width:14px;height:14px;display:grid;place-items:center;color:var(--text-3)}
.ptag button:hover{color:var(--text)}
.ptag svg{width:10px;height:10px}
.inline-input{
  height:25px;width:104px;padding:0 8px;border-radius:999px;border:1px solid var(--line);
  font-size:11.5px;background:var(--bg)
}
.inline-input::placeholder{color:var(--text-3)}
.inline-input:focus{border-color:var(--accent)}
.meta-list{display:flex;flex-direction:column;gap:0;border-top:1px solid var(--line)}
.meta-list div{display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-bottom:1px solid var(--line);font-size:12px}
.meta-list dt{color:var(--text-3);flex:0 0 auto}
.meta-list dd{color:var(--text-2);text-align:right;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-family:var(--mono);font-size:11.5px}
.stars{display:flex;gap:4px}
.stars button{width:22px;height:22px;display:grid;place-items:center;color:var(--text-3)}
.stars button svg{width:14px;height:14px;transition:transform .15s var(--ease)}
.stars button.on{color:var(--text)}
.stars button:hover svg{transform:scale(1.15)}
.drawer-foot{
  flex:0 0 auto;padding:10px 14px 14px;border-top:1px solid var(--line);display:flex;gap:8px;
  background:var(--panel)
}
.drawer-foot .btn{flex:1;justify-content:center}
.danger-text{color:#FF6B6B}

/* ---------- 全屏查看 ---------- */
.viewer{
  position:fixed;inset:0;z-index:60;background:#050608;display:none;
  grid-template-rows:52px minmax(0,1fr) 56px;
}
.viewer.on{display:grid}
.viewer-top{display:flex;align-items:center;gap:12px;padding:0 16px;color:#E8EAED}
.viewer-top .name{font-size:13px;flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;color:#B9BEC6}
.viewer-top button,.viewer-bot button{
  width:32px;height:32px;display:grid;place-items:center;border-radius:7px;color:#C6CBD2;transition:.16s
}
.viewer-top button:hover,.viewer-bot button:hover{background:rgba(255,255,255,.08);color:#fff}
.viewer-top svg,.viewer-bot svg{width:17px;height:17px}
.viewer-stage{position:relative;display:grid;place-items:center;overflow:hidden;padding:0 70px;min-height:0;min-width:0}
.viewer-stage img{max-width:100%;max-height:100%;min-height:0;object-fit:contain;transition:transform .3s var(--ease);cursor:zoom-in}
.viewer-stage img.zoom{transform:scale(1.9);cursor:zoom-out}
.navbtn{
  position:absolute;top:50%;transform:translateY(-50%);width:44px;height:44px;border-radius:50%;
  display:grid;place-items:center;background:rgba(255,255,255,.06);color:#DDE0E4;backdrop-filter:blur(6px)
}
.navbtn:hover{background:rgba(255,255,255,.14)}
.navbtn.l{left:16px}.navbtn.r{right:16px}
.navbtn svg{width:20px;height:20px}
.viewer-bot{display:flex;align-items:center;gap:10px;padding:0 18px;border-top:1px solid rgba(255,255,255,.08);color:#8D939C}
.viewer-bot .idx{font-family:var(--mono);font-size:12px}
.viewer-bot .spacer{flex:1}
.viewer-bot .thumbstrip{display:flex;gap:5px;overflow-x:auto;max-width:50%;padding:6px 0;scrollbar-width:none}
.viewer-bot .thumbstrip::-webkit-scrollbar{height:0}
.viewer-bot .thumbstrip img{width:32px;height:32px;object-fit:cover;border-radius:4px;opacity:.5;cursor:pointer;border:1px solid transparent;flex:0 0 auto}
.viewer-bot .thumbstrip img.on{opacity:1;border-color:var(--accent)}

/* ---------- 导入进度 ---------- */
.progress{
  position:fixed;right:22px;bottom:22px;width:300px;z-index:70;padding:13px 14px;
  background:var(--elev);border:1px solid var(--line-2);border-radius:12px;box-shadow:var(--shadow);
  display:none;
}
.progress.on{display:block;animation:rise .3s var(--ease)}
@keyframes rise{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.progress-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:9px}
.progress-top b{font-size:12px;font-weight:550}
.progress-top span{font-family:var(--mono);font-size:11px;color:var(--text-3)}
.scan{height:3px;background:var(--line);border-radius:3px;overflow:hidden;position:relative}
.scan i{display:block;height:100%;background:var(--accent);transition:width .3s var(--ease)}
.progress .sub{margin-top:8px;font-size:10.5px;color:var(--text-3);display:flex;justify-content:space-between;font-family:var(--mono)}

/* ---------- 弹层 / 菜单 ---------- */
.pop{
  position:fixed;z-index:80;min-width:168px;padding:5px;border-radius:10px;
  background:var(--elev);border:1px solid var(--line-2);box-shadow:var(--shadow);display:none;
}
.pop.on{display:block;animation:rise .16s var(--ease)}
.pop button{display:flex;align-items:center;gap:8px;width:100%;height:32px;padding:0 9px;border-radius:6px;font-size:12.5px;color:var(--text-2);text-align:left}
.pop button:hover{background:var(--hover);color:var(--text)}
.pop button svg{width:14px;height:14px}
.pop .sep{height:1px;background:var(--line);margin:4px 0}
.pop button.on{color:var(--text);font-weight:600}
.pop button.on::after{content:"·";margin-left:auto;color:var(--accent)}

/* toast */
.toast{
  position:fixed;left:50%;bottom:112px;transform:translate(-50%,10px);z-index:90;
  padding:9px 15px;border-radius:999px;background:var(--elev);border:1px solid var(--line-2);
  font-size:12.5px;color:var(--text);box-shadow:var(--shadow);opacity:0;pointer-events:none;
  transition:.24s var(--ease);white-space:nowrap
}
.toast.on{opacity:1;transform:translate(-50%,0)}

/* 工具箱 / 导出转换 */
.modal-card.wide{width:min(540px,100%)}
.cv-row{display:flex;align-items:flex-start;gap:12px;margin-bottom:16px}
.cv-row > label{width:64px;flex:0 0 auto;font-size:12px;color:var(--text-3);padding-top:6px}
.cv-row .grow{flex:1;min-width:0;display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.cv-select{
  height:32px;padding:0 8px;border:1px solid var(--line);border-radius:6px;
  background:var(--bg);font-size:12.5px;color:var(--text);min-width:120px
}
.cv-select:focus{border-color:var(--accent);outline:none}
input[type=range]{
  -webkit-appearance:none;appearance:none;height:4px;border-radius:2px;
  background:var(--line);flex:1;min-width:120px;cursor:pointer
}
input[type=range]::-webkit-slider-thumb{
  -webkit-appearance:none;width:14px;height:14px;border-radius:50%;
  background:var(--text);box-shadow:0 0 0 1px var(--bg)
}
.range-val{font-family:var(--mono);font-size:12px;width:38px;text-align:right;color:var(--text-2)}
.cv-hint{font-size:11px;color:var(--text-3);margin:-6px 0 16px 76px;line-height:1.5}
.modal-card .cv-status{margin-top:14px;display:none}
.modal-card .cv-status.on{display:block}
.cv-status .cv-track{height:3px;background:var(--line);border-radius:3px;overflow:hidden}
.cv-status .cv-track i{display:block;height:100%;width:0;background:var(--accent);transition:width .25s var(--ease)}
.cv-status p{margin:7px 0 0;font-size:11px;color:var(--text-3);font-family:var(--mono);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}

/* 视频工具 */
.vid-drop{
  display:flex;align-items:center;gap:12px;padding:13px;margin-bottom:16px;
  border:1px dashed var(--line-2);border-radius:10px;transition:.18s;cursor:pointer
}
.vid-drop:hover{border-color:var(--text-3);background:var(--hover)}
.vid-drop.hot{border-color:var(--accent);background:color-mix(in srgb,var(--accent) 8%,transparent)}
.vid-drop .ico{width:28px;height:28px;color:var(--text-3);flex:0 0 auto}
.vid-drop .info{flex:1;min-width:0}
.vid-drop b{display:block;font-size:13px;font-weight:550;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.vid-drop span{display:block;font-size:11px;color:var(--text-3);font-family:var(--mono);margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}

/* 状态栏 */
.statusbar{
  flex:0 0 auto;height:34px;display:flex;align-items:center;gap:14px;padding:0 20px;
  border-top:1px solid var(--line);font-size:11px;color:var(--text-3);font-family:var(--mono)
}
.statusbar .spacer{flex:1}
.statusbar .live{display:flex;align-items:center;gap:6px;color:var(--text-2)}
.statusbar .live i{width:5px;height:5px;border-radius:50%;background:var(--accent);box-shadow:0 0 0 3px color-mix(in srgb,var(--accent) 18%,transparent)}

/* ---------- 相册弹窗 ---------- */
.modal{
  position:fixed;inset:0;z-index:75;background:var(--scrim);backdrop-filter:blur(10px);
  display:none;place-items:center;padding:24px;
}
.modal.on{display:grid}
.modal-card{
  width:min(400px,100%);background:var(--panel);border:1px solid var(--line-2);border-radius:var(--r-lg);
  padding:20px;box-shadow:var(--shadow);animation:rise .22s var(--ease);max-height:92vh;overflow-y:auto
}
.modal-card h3{font-size:16px;font-weight:600;margin-bottom:4px}
.modal-card p{font-size:12px;color:var(--text-2);margin-bottom:16px}
.modal-card input[type=text]{
  width:100%;height:38px;padding:0 11px;border:1px solid var(--line);border-radius:var(--r-md);
  background:var(--bg);font-size:13px
}
.modal-card input[type=text]:focus{border-color:var(--accent);outline:none}
.modal-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:18px}
.modal-card .tall{max-height:44vh;overflow:auto;display:flex;flex-direction:column;gap:2px;margin:0 -6px}
.modal-card .tall button{display:flex;align-items:center;gap:9px;padding:9px 8px;border-radius:7px;font-size:13px;text-align:left;color:var(--text-2)}
.modal-card .tall button:hover{background:var(--hover);color:var(--text)}
.modal-card .tall svg{width:15px;height:15px;color:var(--text-3)}

/* ---------- 响应式 ---------- */
@media (max-width:1180px){ :root{--side-w:212px} }
@media (max-width:900px){
  :root{--side-w:0px}
  .app{grid-template-columns:minmax(0,1fr)}
  .app.withdrawer .main{margin-right:0}
  .sidebar{position:fixed;top:0;bottom:0;left:0;width:248px;z-index:50;transform:translateX(-101%);transition:transform .3s var(--ease);box-shadow:24px 0 60px rgba(0,0,0,.3)}
  .sidebar.on{transform:none}
  .drawer{width:100vw;max-width:100vw}
  .search{width:150px}
  .search:focus-within{width:180px}
  .viewer-stage{padding:0 12px}
  .navbtn{display:none}
}
@media (prefers-reduced-motion:reduce){
  *{transition-duration:.01ms!important;animation-duration:.01ms!important;scroll-behavior:auto!important}
}

/* ---------- 启动动画 ---------- */
.splash{
  position:fixed;inset:0;z-index:9990;background:#08090b;
  display:grid;place-items:center;overflow:hidden;
  transition:opacity .46s cubic-bezier(.16,.84,.36,1);
}
.splash.out{opacity:0;pointer-events:none}
.splash .sblob{
  position:absolute;width:560px;height:560px;border-radius:50%;
  background:radial-gradient(circle,rgba(92,155,255,.26) 0%,rgba(92,155,255,.10) 38%,rgba(92,155,255,0) 66%);
  filter:blur(64px);opacity:0;animation:splashBlob 1.5s cubic-bezier(.16,.84,.36,1) .08s forwards;
}
@keyframes splashBlob{
  0%{opacity:0;transform:scale(.82)}
  55%{opacity:1;transform:scale(1.04)}
  100%{opacity:.55;transform:scale(1)}
}
.splash .smark{position:relative;display:flex;flex-direction:column;align-items:center;gap:20px;opacity:0;animation:splashMark .72s cubic-bezier(.16,.84,.36,1) .12s forwards}
@keyframes splashMark{
  0%{opacity:0;transform:translateY(8px) scale(.97)}
  100%{opacity:1;transform:none}
}
.splash .smark svg{width:78px;height:78px;color:#e8eaee}
.splash .smark svg .ring{transform-box:fill-box;transform-origin:center;transform:scale(.6);opacity:.2;animation:splashRing .9s cubic-bezier(.16,.84,.36,1) .18s forwards}
@keyframes splashRing{
  0%{transform:scale(.6);opacity:.2}
  60%{opacity:1}
  100%{transform:scale(1);opacity:1}
}
.splash .sword{display:flex;flex-direction:column;align-items:center;gap:7px}
.splash .sword b{
  font-size:22px;font-weight:600;letter-spacing:.26em;color:#f2f4f7;text-indent:.26em;
  opacity:0;animation:splashWord .8s cubic-bezier(.16,.84,.36,1) .34s forwards;
}
.splash .sword span{
  font-size:11px;letter-spacing:.34em;text-indent:.34em;color:#8b929c;
  opacity:0;animation:splashWord .8s cubic-bezier(.16,.84,.36,1) .46s forwards;
}
@keyframes splashWord{
  0%{opacity:0;letter-spacing:.42em;transform:translateY(4px)}
  100%{opacity:1;transform:none}
}
.splash .sinfo{
  display:flex;flex-direction:column;align-items:center;gap:5px;margin-top:6px;text-align:center;
  opacity:0;animation:splashWord .8s cubic-bezier(.16,.84,.36,1) .58s forwards;
}
.splash .sinfo .sver{
  font-size:10.5px;letter-spacing:.14em;color:#9aa1ab;font-family:var(--mono);
}
.splash .sinfo .sauthor{
  font-size:11.5px;letter-spacing:.06em;color:#c3c8d0;
}
.splash .sinfo .suid{
  font-size:10px;letter-spacing:.08em;color:#6f767f;font-family:var(--mono);
}
.splash .sline{
  position:absolute;left:50%;transform:translateX(-50%);bottom:calc(50% - 152px);
  width:132px;height:1px;background:rgba(255,255,255,.10);overflow:hidden;border-radius:1px;
}
.splash .sline i{
  display:block;height:100%;width:0;background:linear-gradient(90deg,rgba(92,155,255,0),#5c9bff);
  animation:splashLine 1.05s cubic-bezier(.3,.7,.2,1) .2s forwards;
}
@keyframes splashLine{ to{width:100%} }
@media (prefers-reduced-motion: reduce){
  .splash .sblob,.splash .smark,.splash .sword b,.splash .sword span,.splash .smark svg .ring{animation:none;opacity:1;transform:none}
  .splash .sline i{animation:none;width:100%}
}

/* ============ 玻璃材质（最终覆盖） ============ */
.sidebar::after,.drawer::after,.modal-card::after{
  content:"";position:absolute;inset:0;pointer-events:none;z-index:0;border-radius:inherit;
  background:linear-gradient(145deg,rgba(255,255,255,.055) 0%,rgba(255,255,255,.012) 26%,transparent 52%,rgba(255,255,255,.02) 100%);
}
.sidebar{background:var(--glass)!important;border-right:1px solid var(--glass-line);box-shadow:inset 0 1px 0 var(--glass-hi)}
.topbar{background:var(--glass)!important;border-bottom:1px solid var(--glass-line);box-shadow:inset 0 1px 0 var(--glass-hi)}
.drawer{background:var(--glass-2)!important;border-left:1px solid var(--glass-line)}
.modal-card{
  position:relative;background:var(--glass-2)!important;border:1px solid var(--glass-line);
  box-shadow:var(--shadow),inset 0 1px 0 var(--glass-hi);
  animation:liquidPop .34s cubic-bezier(.18,1.3,.34,1)!important;
}
.pop{background:var(--glass-2)!important;border:1px solid var(--glass-line)}
.toast{background:var(--glass-2)!important;border:1px solid var(--glass-line);box-shadow:0 16px 38px rgba(0,0,0,.3),inset 0 1px 0 var(--glass-hi)}
.selbar{background:var(--glass-2)!important;border:1px solid var(--glass-line);box-shadow:0 18px 40px rgba(0,0,0,.28),inset 0 1px 0 var(--glass-hi)}
.drawer{transition:transform .46s cubic-bezier(.22,1,.36,1)!important}
@keyframes liquidPop{0%{opacity:0;transform:translateY(12px) scale(.94)}62%{opacity:1;transform:translateY(-1px) scale(1.006)}100%{opacity:1;transform:none}}
</style>
</head>
<body>
<div class="bg" aria-hidden="true"><i class="b1"></i><i class="b2"></i><i class="b3"></i></div>
<div class="splash" id="splash" aria-hidden="true">
  <div class="sblob"></div>
  <div class="smark">
    <svg viewBox="0 0 64 64" fill="none" aria-hidden="true">
      <g stroke="currentColor" stroke-width="2.4" stroke-linecap="round" opacity=".9">
        <path d="M8 20V10a2 2 0 0 1 2-2h10"/>
        <path d="M56 20V10a2 2 0 0 0-2-2h-10"/>
        <path d="M8 44v10a2 2 0 0 0 2 2h10"/>
        <path d="M56 44v10a2 2 0 0 1-2 2h-10"/>
      </g>
      <circle class="ring" cx="32" cy="32" r="11.5" stroke="#5c9bff" stroke-width="2.2" opacity=".95"/>
      <circle cx="32" cy="32" r="3.2" fill="#f2f4f7"/>
    </svg>
    <div class="sword"><b>CC</b><span>图库管理</span></div>
    <div class="sinfo">
      <span class="sver" data-ver>v1.0.0</span>
      <span class="sauthor" data-author>bilibili彩CAN</span>
      <span class="suid" data-uid>UID:1253361932</span>
    </div>
  </div>
  <div class="sline"><i></i></div>
</div>
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="i-grid" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7" rx="1.5" stroke="currentColor" stroke-width="1.6" fill="none"/><rect x="14" y="3" width="7" height="7" rx="1.5" stroke="currentColor" stroke-width="1.6" fill="none"/><rect x="3" y="14" width="7" height="7" rx="1.5" stroke="currentColor" stroke-width="1.6" fill="none"/><rect x="14" y="14" width="7" height="7" rx="1.5" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-clock" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M12 7v5l3.2 2" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-star" viewBox="0 0 24 24"><path d="M12 3.6l2.6 5.4 5.9.8-4.3 4.1 1 5.9L12 17l-5.2 2.8 1-5.9-4.3-4.1 5.9-.8z" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-star-fill" viewBox="0 0 24 24"><path d="M12 3.6l2.6 5.4 5.9.8-4.3 4.1 1 5.9L12 17l-5.2 2.8 1-5.9-4.3-4.1 5.9-.8z" fill="currentColor"/></symbol>
    <symbol id="i-user" viewBox="0 0 24 24"><circle cx="12" cy="8" r="3.6" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M4.8 20c.6-3.7 3.5-5.6 7.2-5.6s6.6 1.9 7.2 5.6" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-paw" viewBox="0 0 24 24"><ellipse cx="7" cy="8.5" rx="2.1" ry="2.7" stroke="currentColor" stroke-width="1.5" fill="none"/><ellipse cx="12" cy="6.6" rx="2.1" ry="2.9" stroke="currentColor" stroke-width="1.5" fill="none"/><ellipse cx="17" cy="8.5" rx="2.1" ry="2.7" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M12 11.4c3 0 5.2 2.2 5.2 4.3 0 1.9-1.5 3.1-3.3 3.1-1 0-1.4-.4-1.9-.4s-.9.4-1.9.4c-1.8 0-3.3-1.2-3.3-3.1 0-2.1 2.2-4.3 5.2-4.3z" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-mountain" viewBox="0 0 24 24"><path d="M3 19l6-9 4.2 6.2 2.6-3.4L21 19z" stroke="currentColor" stroke-width="1.6" fill="none"/><circle cx="17.6" cy="6.4" r="1.9" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-build" viewBox="0 0 24 24"><rect x="4" y="3.5" width="7" height="17" stroke="currentColor" stroke-width="1.6" fill="none"/><rect x="13" y="8" width="7" height="12.5" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M6.4 7h2.2M6.4 10.6h2.2M6.4 14.2h2.2M15.4 11.6h2.2M15.4 15.2h2.2" stroke="currentColor" stroke-width="1.3" fill="none"/></symbol>
    <symbol id="i-food" viewBox="0 0 24 24"><path d="M4 12h16c0 4.4-3.6 7.5-8 7.5S4 16.4 4 12z" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M8 20.5h8M3.4 12h17.2" stroke="currentColor" stroke-width="1.4" fill="none"/><path d="M9 4v4M12 3.4v4.6M15 4v4" stroke="currentColor" stroke-width="1.4" fill="none"/></symbol>
    <symbol id="i-dots" viewBox="0 0 24 24"><circle cx="6" cy="12" r="1.6" fill="currentColor"/><circle cx="12" cy="12" r="1.6" fill="currentColor"/><circle cx="18" cy="12" r="1.6" fill="currentColor"/></symbol>
    <symbol id="i-search" viewBox="0 0 24 24"><circle cx="10.5" cy="10.5" r="6.6" stroke="currentColor" stroke-width="1.7" fill="none"/><path d="M15.4 15.4L20 20" stroke="currentColor" stroke-width="1.7"/></symbol>
    <symbol id="i-plus" viewBox="0 0 24 24"><path d="M12 4.5v15M4.5 12h15" stroke="currentColor" stroke-width="1.7"/></symbol>
    <symbol id="i-sun" viewBox="0 0 24 24"><circle cx="12" cy="12" r="4.2" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M12 2.6v2.4M12 19v2.4M2.6 12h2.4M19 12h2.4M5.4 5.4l1.7 1.7M16.9 16.9l1.7 1.7M18.6 5.4l-1.7 1.7M7.1 16.9l-1.7 1.7" stroke="currentColor" stroke-width="1.5"/></symbol>
    <symbol id="i-moon" viewBox="0 0 24 24"><path d="M20 14.4A8.6 8.6 0 1 1 9.6 4a6.9 6.9 0 0 0 10.4 10.4z" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-close" viewBox="0 0 24 24"><path d="M6 6l12 12M18 6L6 18" stroke="currentColor" stroke-width="1.7"/></symbol>
    <symbol id="i-chevron" viewBox="0 0 24 24"><path d="M9 5l7 7-7 7" stroke="currentColor" stroke-width="1.7" fill="none"/></symbol>
    <symbol id="i-chevron-l" viewBox="0 0 24 24"><path d="M15 5l-7 7 7 7" stroke="currentColor" stroke-width="1.7" fill="none"/></symbol>
    <symbol id="i-folder" viewBox="0 0 24 24"><path d="M3.5 7.5a2 2 0 0 1 2-2h3.4l2 2.5h7.6a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2h-13a2 2 0 0 1-2-2z" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-file" viewBox="0 0 24 24"><path d="M6 3.5h7l5 5v12H6z" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M13 3.5V9h5" stroke="currentColor" stroke-width="1.4" fill="none"/></symbol>
    <symbol id="i-image" viewBox="0 0 24 24"><rect x="3.4" y="4.6" width="17.2" height="14.8" rx="2" stroke="currentColor" stroke-width="1.6" fill="none"/><circle cx="8.6" cy="9.6" r="1.6" fill="currentColor"/><path d="M4.4 17l5-5.4 3.4 3.6 2.8-2.4 4 4.2" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-trash" viewBox="0 0 24 24"><path d="M4.6 7h14.8M9.4 7V4.8h5.2V7M6.4 7l.9 12.2h10.4l.9-12.2" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-check" viewBox="0 0 24 24"><path d="M5 12.6l4.4 4.4L19 7.4" stroke="currentColor" stroke-width="1.9" fill="none"/></symbol>
    <symbol id="i-check-circle" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M7.6 12.4l3 3 5.8-6" stroke="currentColor" stroke-width="1.7" fill="none"/></symbol>
    <symbol id="i-sort" viewBox="0 0 24 24"><path d="M7 4v16M7 20l-3-3.4M7 20l3-3.4M17 20V4M17 4l3 3.4M17 4l-3 3.4" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-select" viewBox="0 0 24 24"><rect x="3.6" y="3.6" width="7" height="7" rx="1.4" stroke="currentColor" stroke-width="1.5" fill="none"/><rect x="3.6" y="13.4" width="7" height="7" rx="1.4" stroke="currentColor" stroke-width="1.5" fill="none"/><rect x="13.4" y="3.6" width="7" height="7" rx="1.4" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M14.2 17h6.2M17.3 13.9v6.2" stroke="currentColor" stroke-width="1.5"/></symbol>
    <symbol id="i-tag" viewBox="0 0 24 24"><path d="M11.4 3.6H4.6a1 1 0 0 0-1 1v6.8l9.5 9.5a1.4 1.4 0 0 0 2 0l6.4-6.4a1.4 1.4 0 0 0 0-2z" stroke="currentColor" stroke-width="1.5" fill="none"/><circle cx="8.4" cy="8.4" r="1.5" fill="currentColor"/></symbol>
    <symbol id="i-fav" viewBox="0 0 24 24"><path d="M12 20s-7.4-4.6-8.6-9.2c-.9-3.4 2.6-6.4 5.6-4.8 1.3.7 2.1 2 3 3.2.9-1.2 1.7-2.5 3-3.2 3-1.6 6.5 1.4 5.6 4.8C19.4 15.4 12 20 12 20z" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-info" viewBox="0 0 24 24"><circle cx="12" cy="12" r="8.6" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M12 11v5.6M12 7.6v.6" stroke="currentColor" stroke-width="1.6"/></symbol>
    <symbol id="i-zoom" viewBox="0 0 24 24"><circle cx="10.6" cy="10.6" r="6.4" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M15.2 15.2L20 20M8.2 10.6h4.8" stroke="currentColor" stroke-width="1.6"/></symbol>
    <symbol id="i-density" viewBox="0 0 24 24"><rect x="3.5" y="3.5" width="7" height="7" rx="1.2" fill="currentColor" opacity=".9"/><rect x="13.5" y="3.5" width="7" height="7" rx="1.2" fill="currentColor" opacity=".45"/><rect x="3.5" y="13.5" width="7" height="7" rx="1.2" fill="currentColor" opacity=".45"/><rect x="13.5" y="13.5" width="7" height="7" rx="1.2" fill="currentColor" opacity=".9"/></symbol>
    <symbol id="i-film" viewBox="0 0 24 24"><rect x="3.2" y="4.6" width="17.6" height="14.8" rx="2" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M7.4 4.6v14.8M16.6 4.6v14.8" stroke="currentColor" stroke-width="1.3"/><path d="M10.6 9.2l3.6 2.8-3.6 2.8z" fill="currentColor"/></symbol>
    <symbol id="i-convert" viewBox="0 0 24 24"><path d="M4.6 9.4a7.6 7.6 0 0 1 13-3.2" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M17.9 2.9v3.8h-3.8" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M19.4 14.6a7.6 7.6 0 0 1-13 3.2" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M6.1 21.1v-3.8h3.8" stroke="currentColor" stroke-width="1.6" fill="none"/></symbol>
    <symbol id="i-rotate" viewBox="0 0 24 24"><rect x="6.6" y="6.6" width="10.8" height="10.8" rx="1.6" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M9.4 3.6H4.2v5.2" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M4.4 8.6a7.6 7.6 0 0 1 12.4-2.4" stroke="currentColor" stroke-width="1.5" fill="none"/></symbol>
    <symbol id="i-audio" viewBox="0 0 24 24"><path d="M4 12v0M7 9v6M10 6.4v11.2M13 8.6v6.8M16 5.4v13.2M19 10v4" stroke="currentColor" stroke-width="1.6" fill="none" stroke-linecap="round"/></symbol>
    <symbol id="i-play" viewBox="0 0 24 24"><path d="M9.2 6.4l8.2 5.6-8.2 5.6z" fill="currentColor"/></symbol>
    <symbol id="i-menu" viewBox="0 0 24 24"><path d="M4 7h16M4 12h16M4 17h16" stroke="currentColor" stroke-width="1.6"/></symbol>
    <symbol id="i-album" viewBox="0 0 24 24"><rect x="3.4" y="4.4" width="17.2" height="15.2" rx="2" stroke="currentColor" stroke-width="1.6" fill="none"/><path d="M7 4.4v15.2" stroke="currentColor" stroke-width="1.4"/><circle cx="14.4" cy="9.6" r="1.5" fill="currentColor"/><path d="M17.6 16l-3-3.4-2.2 2.5-1.4-1.4" stroke="currentColor" stroke-width="1.4" fill="none"/></symbol>
    <symbol id="i-ai" viewBox="0 0 24 24"><path d="M12 3.2l1.9 4.6 4.9 1.9-4.9 1.9L12 16.2l-1.9-4.6L5.2 9.7l4.9-1.9z" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M18.6 15.4l.8 2 2 .8-2 .8-.8 2-.8-2-2-.8 2-.8z" stroke="currentColor" stroke-width="1.3" fill="none"/></symbol>
  </defs>
</svg>

<div class="app">
  <!-- ===== 侧栏 ===== -->
  <aside class="sidebar" id="sidebar">
    <div class="brand">
      <div class="brand-mark"><svg><use href="#i-image" xlink:href="#i-image"/></svg></div>
      <div class="brand-name"><b>CC</b><span>图库管理</span></div>
    </div>
    <nav class="nav">
      <div class="nav-group">
        <div class="nav-label">图库</div>
        <button class="nav-item" data-view="all" aria-current="true">
          <svg class="ico"><use href="#i-grid" xlink:href="#i-grid"/></svg><span class="txt">全部照片</span><span class="cnt" id="cAll">0</span>
        </button>
        <button class="nav-item" data-view="recent">
          <svg class="ico"><use href="#i-clock" xlink:href="#i-clock"/></svg><span class="txt">最近导入</span><span class="cnt" id="cRecent">0</span>
        </button>
        <button class="nav-item" data-view="fav">
          <svg class="ico"><use href="#i-star" xlink:href="#i-star"/></svg><span class="txt">收藏</span><span class="cnt" id="cFav">0</span>
        </button>
        <button class="nav-item" data-view="video">
          <svg class="ico"><use href="#i-film" xlink:href="#i-film"/></svg><span class="txt">视频</span><span class="cnt" id="cVideo">0</span>
        </button>
        <button class="nav-item" data-view="audio">
          <svg class="ico"><use href="#i-audio" xlink:href="#i-audio"/></svg><span class="txt">音频</span><span class="cnt" id="cAudio">0</span>
        </button>
      </div>
      <div class="nav-group">
        <div class="nav-label">智能分区 <span style="font-size:10px;color:var(--text-3)">自动</span></div>
        <button class="nav-item" data-view="cat:person"><svg class="ico"><use href="#i-user" xlink:href="#i-user"/></svg><span class="txt">人物</span><span class="cnt" data-count="person">0</span></button>
        <button class="nav-item" data-view="cat:animal"><svg class="ico"><use href="#i-paw" xlink:href="#i-paw"/></svg><span class="txt">动物</span><span class="cnt" data-count="animal">0</span></button>
        <button class="nav-item" data-view="cat:scenery"><svg class="ico"><use href="#i-mountain" xlink:href="#i-mountain"/></svg><span class="txt">风景</span><span class="cnt" data-count="scenery">0</span></button>
        <button class="nav-item" data-view="cat:building"><svg class="ico"><use href="#i-build" xlink:href="#i-build"/></svg><span class="txt">建筑</span><span class="cnt" data-count="building">0</span></button>
        <button class="nav-item" data-view="cat:food"><svg class="ico"><use href="#i-food" xlink:href="#i-food"/></svg><span class="txt">美食</span><span class="cnt" data-count="food">0</span></button>
        <button class="nav-item" data-view="cat:other"><svg class="ico"><use href="#i-dots" xlink:href="#i-dots"/></svg><span class="txt">其他</span><span class="cnt" data-count="other">0</span></button>
      </div>
      <div class="nav-group">
        <div class="nav-label">相册 <button class="tool" id="newAlbumBtn" style="width:22px;height:22px" title="新建相册"><svg style="width:13px;height:13px"><use href="#i-plus" xlink:href="#i-plus"/></svg></button></div>
        <div id="albumList"></div>
      </div>
      <div class="nav-group">
        <div class="nav-label">工具</div>
        <button class="nav-item" id="convertBtn" title="导出、转换格式、压缩尺寸">
          <svg class="ico"><use href="#i-convert" xlink:href="#i-convert"/></svg><span class="txt">导出与转换</span>
        </button>
        <button class="nav-item" id="videoBtn" title="视频转格式、提取音轨">
          <svg class="ico"><use href="#i-film" xlink:href="#i-film"/></svg><span class="txt">视频工具</span>
        </button>
      </div>
    </nav>
    <div class="side-foot">
      <div class="storage">
        <div class="storage-top"><span>本地图库</span><span id="storeText" class="mono">0 张 · 0 MB</span></div>
        <div class="storage-bar"><i id="storeBar" style="width:0%"></i></div>
      </div>
      <div class="note">照片只保存在本机浏览器存储中，不上传、不联网。清除浏览数据会移除图库。</div>
      <div class="side-meta"><span data-ver>v1.0.0</span></div>
    </div>
  </aside>

  <!-- ===== 主区 ===== -->
  <main class="main">
    <header class="topbar">
      <div class="tool" id="menuBtn" style="display:none" title="菜单"><svg><use href="#i-menu" xlink:href="#i-menu"/></svg></div>
      <div class="crumb">
        <h1 id="viewTitle">全部照片</h1>
        <p id="viewMeta">0 张照片</p>
      </div>
      <div class="search">
        <svg><use href="#i-search" xlink:href="#i-search"/></svg>
        <input id="searchInput" type="search" placeholder="搜索文件名、人物、标签" autocomplete="off">
        <kbd>Ctrl K</kbd>
      </div>
      <div class="tool-div"></div>
      <button class="tool" id="sortBtn" title="排序"><svg><use href="#i-sort" xlink:href="#i-sort"/></svg></button>
      <button class="tool" id="densityBtn" title="缩略图大小"><svg><use href="#i-density" xlink:href="#i-density"/></svg></button>
      <button class="tool" id="selectBtn" title="批量选择"><svg><use href="#i-select" xlink:href="#i-select"/></svg></button>
      <button class="tool" id="themeBtn" title="切换明暗主题"><svg><use href="#i-sun" xlink:href="#i-sun"/></svg></button>
      <button class="btn" id="importBtn"><svg><use href="#i-plus" xlink:href="#i-plus"/></svg>导入照片</button>
    </header>

    <div class="subbar" id="subbar">
      <div class="spacer"></div>
    </div>

    <div class="content" id="content">
      <div class="content-inner" id="contentInner"></div>
      <div class="selbar" id="selbar">
        <span class="count">已选 <b id="selCount">0</b> 张</span>
        <div class="vline"></div>
        <button id="selCat"><svg><use href="#i-tag" xlink:href="#i-tag"/></svg>设置分区</button>
        <button id="selFav"><svg><use href="#i-star" xlink:href="#i-star"/></svg>收藏</button>
        <button id="selRotate"><svg><use href="#i-rotate" xlink:href="#i-rotate"/></svg>旋转</button>
        <button id="selConvert"><svg><use href="#i-convert" xlink:href="#i-convert"/></svg>转换</button>
        <button id="selAlbum"><svg><use href="#i-album" xlink:href="#i-album"/></svg>加入相册</button>
        <div class="vline"></div>
        <button class="danger" id="selRemove"><svg><use href="#i-trash" xlink:href="#i-trash"/></svg>移出图库</button>
        <button id="selClear"><svg><use href="#i-close" xlink:href="#i-close"/></svg></button>
      </div>
    </div>

    <footer class="statusbar">
      <div class="live"><i></i><span id="statusLive">本地模式</span></div>
      <span id="statusCount">0 张照片</span>
      <span class="spacer"></span>
      <span id="statusSize">0 MB</span>
      <span id="statusFilter">无筛选</span>
    </footer>
  </main>
</div>

<!-- ===== 详情抽屉 ===== -->
<aside class="drawer" id="drawer" aria-hidden="true">
  <div class="drawer-head">
    <h3 id="dTitle">照片信息</h3>
    <button class="tool" id="dClose"><svg><use href="#i-close" xlink:href="#i-close"/></svg></button>
  </div>
  <div class="preview" id="dPreview"><img id="dImg" alt=""></div>
  <div class="drawer-body" id="dBody"></div>
  <div class="drawer-foot">
    <button class="btn ghost sm" id="dOpen"><svg><use href="#i-zoom" xlink:href="#i-zoom"/></svg>全屏</button>
    <button class="btn ghost sm" id="dExport"><svg><use href="#i-convert" xlink:href="#i-convert"/></svg>导出</button>
    <button class="btn ghost sm" id="dRemove"><svg><use href="#i-trash" xlink:href="#i-trash"/></svg>移出</button>
  </div>
</aside>

<!-- ===== 全屏查看 ===== -->
<div class="viewer" id="viewer">
  <div class="viewer-top">
    <button id="vClose"><svg><use href="#i-close" xlink:href="#i-close"/></svg></button>
    <span class="name" id="vName"></span>
    <button id="vFav" title="收藏"><svg><use href="#i-star" xlink:href="#i-star"/></svg></button>
    <button id="vInfo" title="信息"><svg><use href="#i-info" xlink:href="#i-info"/></svg></button>
  </div>
  <div class="viewer-stage">
    <button class="navbtn l" id="vPrev"><svg><use href="#i-chevron-l" xlink:href="#i-chevron-l"/></svg></button>
    <img id="vImg" alt="">
    <video id="vVid" controls playsinline preload="metadata"></video>
    <div class="vaudio" id="vAudio"><img id="vAudImg" alt=""><audio id="vAud" controls></audio></div>
    <button class="navbtn r" id="vNext"><svg><use href="#i-chevron" xlink:href="#i-chevron"/></svg></button>
  </div>
  <div class="viewer-bot">
    <span class="idx" id="vIdx">1 / 1</span>
    <span class="spacer"></span>
    <div class="thumbstrip" id="vStrip"></div>
    <span class="spacer"></span>
    <span class="idx" id="vDim"></span>
  </div>
</div>

<!-- ===== 导入进度 ===== -->
<div class="progress" id="progress">
  <div class="progress-top"><b id="pTitle">正在导入</b><span id="pCount">0 / 0</span></div>
  <div class="scan"><i id="pBar" style="width:0%"></i></div>
  <div class="sub"><span id="pName">准备中…</span><span id="pPct">0%</span></div>
</div>

<!-- ===== 浮层菜单 ===== -->
<div class="pop" id="pop"></div>

<!-- ===== 相册弹窗 ===== -->
<div class="modal" id="modal">
  <div class="modal-card" id="modalCard"></div>
</div>

<div class="toast" id="toast"></div>

<input type="file" id="fileInput" accept="image/*,video/*,audio/*,.mkv,.mov,.avi,.m4v,.mts,.flac,.m4a,.wma,.aiff" multiple hidden>
<input type="file" id="dirInput" webkitdirectory directory multiple hidden>
<input type="file" id="videoInput" accept="video/*,.mov,.mkv,.avi,.m4v,.mts" hidden>

<script>
/* ============================================================
   CC 图库管理 · 本地媒体库
   数据全部保存在本机 IndexedDB，不联网、不上传
   ============================================================ */

const APP_VER = 'v1.0.0';
const APP_UID = '1253361932';
const APP_AUTHOR = 'bilibili彩CAN';

function fillAppMeta(){
  document.querySelectorAll('[data-ver]').forEach(el => el.textContent = APP_VER);
  document.querySelectorAll('[data-uid]').forEach(el => el.textContent = 'UID:' + APP_UID);
  document.querySelectorAll('[data-author]').forEach(el => el.textContent = APP_AUTHOR);
}

const CATS = {
  person:     { label:'人物', icon:'i-user' },
  animal:     { label:'动物', icon:'i-paw' },
  scenery:    { label:'风景', icon:'i-mountain' },
  building:   { label:'建筑', icon:'i-build' },
  food:       { label:'美食', icon:'i-food' },
  other:      { label:'其他', icon:'i-dots' }
};
const CAT_KEYS = Object.keys(CATS);
const SORTS = [
  { key:'added_desc', label:'导入时间 · 新→旧' },
  { key:'added_asc',  label:'导入时间 · 旧→新' },
  { key:'name_asc',   label:'文件名 · A→Z' },
  { key:'size_desc',  label:'文件大小 · 大→小' },
  { key:'mtime_desc', label:'拍摄时间 · 新→旧' }
];

const S = {
  view:'all', catFilter:null, personFilter:null, albumId:null,
  search:'', sort:'added_desc', density:'md',
  selectMode:false, selected:new Set(),
  detailId:null, viewerIdx:0,
  photos:[], albums:[]
};
const urlCache = new Map();
let iPad = false;

/* ---------- 小工具 ---------- */
const $ = id => document.getElementById(id);
const fmtSize = n => n < 1024 ? n+' B' : n < 1048576 ? (n/1024).toFixed(0)+' KB' : (n/1048576).toFixed(1)+' MB';
const fmtDate = t => { const d = new Date(t); const p = x => String(x).padStart(2,'0'); return `${d.getFullYear()}-${p(d.getMonth()+1)}-${p(d.getDate())} ${p(d.getHours())}:${p(d.getMinutes())}`; };
const esc = s => String(s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const uid = () => Date.now().toString(36) + Math.random().toString(36).slice(2,8);
const tick = (ms=12) => new Promise(r => setTimeout(r, ms));

function toast(msg){
  const t = $('toast'); t.textContent = msg; t.classList.add('on');
  clearTimeout(t._h); t._h = setTimeout(()=>t.classList.remove('on'), 2200);
}
function photoUrl(p){
  if(urlCache.has(p.id)) return urlCache.get(p.id);
  if(!p.blob) return p.thumb || '';
  const u = URL.createObjectURL(p.blob);
  urlCache.set(p.id, u);
  return u;
}
function dropUrl(id){ if(urlCache.has(id)){ URL.revokeObjectURL(urlCache.get(id)); urlCache.delete(id); } }

/* ---------- IndexedDB ---------- */
const DB_NAME = 'lumen-photo-lib', DB_VER = 1;
let db = null;
function openDB(){
  return new Promise((res, rej) => {
    const req = indexedDB.open(DB_NAME, DB_VER);
    req.onupgradeneeded = e => {
      const d = e.target.result;
      if(!d.objectStoreNames.contains('photos')) d.createObjectStore('photos', { keyPath:'id' });
      if(!d.objectStoreNames.contains('albums')) d.createObjectStore('albums', { keyPath:'id' });
    };
    req.onsuccess = () => { db = req.result; res(db); };
    req.onerror = () => rej(req.error);
  });
}
function store(name, mode){
  return db.transaction(name, mode || 'readonly').objectStore(name);
}
function dbPut(name, val){
  return new Promise((res, rej) => {
    const r = store(name, 'readwrite').put(val);
    r.onsuccess = () => res(val); r.onerror = () => rej(r.error);
  });
}
function dbDel(name, key){
  return new Promise((res, rej) => {
    const r = store(name, 'readwrite').delete(key);
    r.onsuccess = () => res(); r.onerror = () => rej(r.error);
  });
}
function dbAll(name){
  return new Promise((res, rej) => {
    const r = store(name).getAll();
    r.onsuccess = () => res(r.result || []); r.onerror = () => rej(r.error);
  });
}
function dbClear(name){
  return new Promise((res, rej) => {
    const r = store(name, 'readwrite').clear();
    r.onsuccess = () => res(); r.onerror = () => rej(r.error);
  });
}

/* ---------- 图片分析 + 自动分区 ----------
   纯本地启发式视觉分析：肤色占比 → 人物；绿色/天空占比 → 风景；
   暖色高饱和 → 美食；低饱和高边缘 → 建筑。不上传任何图片。
   识别结果可随时手动校正（详情面板）。                         */
function analyzePixels(data, w, h){
  const total = w * h;
  let skin = 0, skinCenter = 0, green = 0, blue = 0, topBlue = 0, warm = 0,
      gray = 0, edge = 0, sat = 0, bright = 0;
  const centerX0 = w * .25, centerX1 = w * .75, centerY0 = h * .2, centerY1 = h * .85;
  for(let y = 0; y < h; y++){
    for(let x = 0; x < w; x++){
      const i = (y * w + x) * 4;
      const r = data[i], g = data[i+1], b = data[i+2], a = data[i+3];
      if(a < 20) continue;
      const mx = Math.max(r,g,b), mn = Math.min(r,g,b), d = mx - mn;
      if(r > 95 && g > 40 && b > 20 && d > 15 && r > g && r > b && Math.abs(r-g) > 15){
        skin++;
        if(x >= centerX0 && x <= centerX1 && y >= centerY0 && y <= centerY1) skinCenter++;
      }
      if(g > r + 8 && g > b + 8 && g > 50) green++;
      if(b > r + 14 && b > g + 2 && b > 80){ blue++; if(y < h * .45) topBlue++; }
      if(r > g + 16 && g >= b && mx > 70) warm++;
      if(d < 12) gray++;
      if(mx > 215) bright++;
      sat += d / 255;
    }
  }
  // 边缘密度（横向梯度）
  for(let y = 0; y < h; y += 2){
    for(let x = 0; x < w - 1; x += 2){
      const i = (y * w + x) * 4, j = i + 4;
      const gx = Math.abs(data[i] - data[j]) + Math.abs(data[i+1] - data[j+1]) + Math.abs(data[i+2] - data[j+2]);
      if(gx > 90) edge++;
    }
  }
  const sampled = Math.ceil(total / 4);
  return {
    skin: skin/total, skinCenter: skinCenter/total, green: green/total,
    blue: blue/total, topBlue: topBlue/total, warm: warm/total,
    gray: gray/total, edge: edge/sampled, sat: sat/total, bright: bright/total
  };
}

function classifyStats(st){
  // 风景：绿植 / 天空 显著
  if(st.green > 0.28 || st.green + st.blue > 0.42 || (st.blue > 0.16 && st.topBlue > 0.08))
    return { cat:'scenery', conf: Math.min(.94, .55 + (st.green + st.blue) * .55) };
  // 美食：高饱和暖色占主导
  if(st.warm > 0.30 && st.sat > 0.40)
    return { cat:'food', conf: Math.min(.84, .45 + st.warm * .8) };
  // 人物：大面积肤色且集中在画面中部
  if(st.skin > 0.09 && st.skinCenter > 0.03)
    return { cat:'person', conf: Math.min(.96, .55 + st.skin * 1.2) };
  // 建筑：低饱和 + 线条密集
  if(st.gray > 0.46 && st.edge > 0.09)
    return { cat:'building', conf: Math.min(.80, .42 + st.edge * 1.4) };
  return { cat:'other', conf: .45 };
}

async function loadBitmap(file){
  if('createImageBitmap' in window){
    try { return await createImageBitmap(file); } catch(e){}
  }
  return await new Promise((res, rej) => {
    const img = new Image();
    const url = URL.createObjectURL(file);
    img.onload = () => { URL.revokeObjectURL(url); res(img); };
    img.onerror = () => { URL.revokeObjectURL(url); rej(new Error('decode failed')); };
    img.src = url;
  });
}

async function analyzeFile(file){
  const bmp = await loadBitmap(file);
  const w = bmp.width || bmp.naturalWidth, h = bmp.height || bmp.naturalHeight;

  // 缩略图（最长边 640）
  const tw = w >= h ? Math.min(640, w) : Math.round(640 * w / h);
  const th = w >= h ? Math.round(640 * h / w) : Math.min(640, h);
  const tc = document.createElement('canvas');
  tc.width = Math.max(1, tw); tc.height = Math.max(1, th);
  const tctx = tc.getContext('2d', { alpha:false });
  tctx.fillStyle = '#111'; tctx.fillRect(0,0,tc.width,tc.height);
  tctx.drawImage(bmp, 0, 0, tc.width, tc.height);
  const thumb = tc.toDataURL('image/jpeg', .78);

  // 分析用小图
  const ac = document.createElement('canvas');
  ac.width = 96; ac.height = 96;
  const actx = ac.getContext('2d', { willReadFrequently:true });
  actx.drawImage(bmp, 0, 0, 96, 96);
  const stats = analyzePixels(actx.getImageData(0,0,96,96).data, 96, 96);
  let auto = classifyStats(stats);
  // 若浏览器提供原生人脸检测（Chrome / Edge），命中人脸时直接判为人物
  if('FaceDetector' in window){
    try {
      const fd = new FaceDetector({ fastMode:true, maxDetectedFaces:5 });
      const faces = await fd.detect(bmp);
      if(faces && faces.length){ auto = { cat:'person', conf:.93 }; }
    } catch(e){}
  }
  if(bmp.close) bmp.close();

  return { w, h, thumb, auto };
}

/* ---------- 导入 ---------- */
const IMAGE_RE = /\.(jpg|jpeg|png|webp|gif|bmp|avif|heic|heif|tif|tiff|svg)$/i;
const VIDEO_RE = /\.(mp4|m4v|mov|webm|mkv|avi|mts|m2ts|wmv|flv|3gp|ts)$/i;
const AUDIO_RE = /\.(mp3|wav|flac|m4a|aac|ogg|oga|opus|wma|aiff|aif|amr)$/i;

function imageLike(f){
  return /image\/(jpeg|png|webp|gif|bmp|avif|svg\+xml)/.test(f.type) || IMAGE_RE.test(f.name);
}
function mediaKind(f){
  const t = (f.type || '').toLowerCase();
  if(t.startsWith('image/')) return 'image';
  if(t.startsWith('video/')) return 'video';
  if(t.startsWith('audio/')) return 'audio';
  if(IMAGE_RE.test(f.name)) return 'image';
  if(VIDEO_RE.test(f.name)) return 'video';
  if(AUDIO_RE.test(f.name)) return 'audio';
  return null;
}
function fmtDur(s){
  s = Math.max(0, Math.round(s || 0));
  const h = Math.floor(s / 3600), m = Math.floor(s / 60) % 60, sec = s % 60;
  if(h) return `${h}:${String(m).padStart(2,'0')}:${String(sec).padStart(2,'0')}`;
  return `${m}:${String(sec).padStart(2,'0')}`;
}
function relPath(f){ return (f.webkitRelativePath || f.name || '').replace(/^\/+/, ''); }

/* 视频 / 音频封面：截帧或画占位 */
function placeholderThumb(label, name){
  const c = document.createElement('canvas'); c.width = 640; c.height = 480;
  const x = c.getContext('2d');
  x.fillStyle = '#0d0f12'; x.fillRect(0, 0, 640, 480);
  x.strokeStyle = '#23272e'; x.lineWidth = 1;
  for(let i = 0; i < 11; i++){ const y = 60 + i * 34; x.beginPath(); x.moveTo(48, y); x.lineTo(592, y); x.stroke(); }
  x.fillStyle = '#5c9bff'; x.font = '600 22px system-ui, -apple-system, sans-serif';
  x.fillText(label, 48, 236);
  x.fillStyle = '#8b9099'; x.font = '400 16px system-ui, -apple-system, sans-serif';
  x.fillText((name || '').slice(0, 32), 48, 272);
  return c.toDataURL('image/jpeg', .8);
}

function waveThumb(buf, name){
  const c = document.createElement('canvas'); c.width = 640; c.height = 640;
  const x = c.getContext('2d');
  x.fillStyle = '#0c0e11'; x.fillRect(0, 0, 640, 640);
  // 参考线
  x.strokeStyle = '#1d2026'; x.lineWidth = 1;
  [200, 260, 320, 380, 440].forEach(y => { x.beginPath(); x.moveTo(40, y); x.lineTo(600, y); x.stroke(); });

  const ch = buf.getChannelData(0);
  const cols = 120, step = Math.max(1, Math.floor(ch.length / cols));
  // 先求峰值再归一化，避免小音量画成一条线
  const peaks = [];
  let max = 0;
  for(let i = 0; i < cols; i++){
    let peak = 0;
    for(let j = 0; j < step; j += 4){
      const val = Math.abs(ch[i * step + j] || 0);
      if(val > peak) peak = val;
    }
    peaks.push(peak);
    if(peak > max) max = peak;
  }
  const norm = max > 0 ? 1 / max : 0;
  const midY = 320;
  for(let i = 0; i < cols; i++){
    const hgt = Math.max(3, Math.min(1, peaks[i] * norm) * 260);
    const px = 40 + i * 4.6;
    x.strokeStyle = i % 2 ? '#5c9bff' : '#4d87e0';
    x.lineWidth = 3;
    x.beginPath(); x.moveTo(px, midY - hgt / 2); x.lineTo(px, midY + hgt / 2); x.stroke();
  }
  x.fillStyle = '#d3d7de'; x.font = '500 18px system-ui, -apple-system, sans-serif';
  x.fillText((name || '').slice(0, 30), 40, 566);
  return c.toDataURL('image/jpeg', .82);
}

async function analyzeVideo(file){
  const url = URL.createObjectURL(file);
  const v = document.createElement('video');
  v.src = url; v.muted = true; v.playsInline = true; v.preload = 'auto';
  v.style.cssText = 'position:fixed;left:-9999px;top:0;width:2px;height:2px;opacity:0;pointer-events:none';
  document.body.appendChild(v);
  let thumb = null, w = 0, h = 0, dur = 0;
  try {
    await new Promise(r => { v.onloadeddata = r; v.onerror = r; setTimeout(r, 15000); });
    w = v.videoWidth || 0; h = v.videoHeight || 0;
    dur = Number.isFinite(v.duration) ? v.duration : 0;
    if(!w || !h) throw new Error('decode failed');
    if(dur > 0){
      await new Promise(r => { v.onseeked = r; v.currentTime = Math.min(0.8, dur * 0.25); setTimeout(r, 2500); });
    }
    const scale = Math.min(1, 640 / Math.max(w, h));
    const cw = Math.max(1, Math.round(w * scale)), chh = Math.max(1, Math.round(h * scale));
    const c = document.createElement('canvas'); c.width = cw; c.height = chh;
    const x = c.getContext('2d');
    x.fillStyle = '#0b0c0e'; x.fillRect(0, 0, cw, chh);
    x.drawImage(v, 0, 0, cw, chh);
    thumb = c.toDataURL('image/jpeg', .74);
  } catch(e){}
  finally { URL.revokeObjectURL(url); v.remove(); }
  return { w, h, dur, thumb: thumb || placeholderThumb('VIDEO · 需系统播放器解码', file.name), auto:{ cat:'other', conf:0 } };
}

async function analyzeAudio(file){
  const url = URL.createObjectURL(file);
  const a = document.createElement('audio');
  a.preload = 'metadata'; a.src = url;
  let dur = 0;
  await new Promise(r => { a.onloadedmetadata = r; a.onerror = r; setTimeout(r, 6000); });
  if(Number.isFinite(a.duration)) dur = a.duration;
  let thumb = null;
  try {
    if(file.size < 160 * 1024 * 1024){
      const ac = new (window.AudioContext || window.webkitAudioContext)();
      const buf = await ac.decodeAudioData(await file.arrayBuffer());
      if(buf.duration) dur = buf.duration;
      thumb = waveThumb(buf, file.name);
      if(ac.close) ac.close();
    }
  } catch(e){}
  URL.revokeObjectURL(url);
  return { w:0, h:0, dur, thumb: thumb || placeholderThumb('AUDIO · 波形不可解析', file.name), auto:{ cat:'other', conf:0 } };
}

async function importFiles(fileList){
  const all = Array.from(fileList || []);
  if(!all.length){ toast('没有选中任何文件'); return; }
  const files = all.map(f => ({ f, kind: mediaKind(f) })).filter(x => x.kind);
  if(!files.length){ toast(`这 ${all.length} 个文件不是支持的图片 / 视频 / 音频`); return; }
  if(!db) await openDB();

  iPad = true;
  $('progress').classList.add('on');
  $('pTitle').textContent = '正在导入';
  let added = 0, dup = 0, failed = 0;
  const existing = new Set(S.photos.map(p => p.key));

  for(let i = 0; i < files.length; i++){
    const f = files[i].f, kind = files[i].kind;
    const bar = Math.round(i / files.length * 100);
    $('pBar').style.width = bar + '%';
    $('pPct').textContent = bar + '%';
    $('pCount').textContent = `${i+1} / ${files.length}`;
    $('pName').textContent = f.name;

    const rel = relPath(f);
    const key = rel + '|' + f.size + '|' + (f.lastModified || 0);
    if(existing.has(key)){ dup++; continue; }
    existing.add(key);

    try {
      let info;
      if(kind === 'video') info = await analyzeVideo(f);
      else if(kind === 'audio') info = await analyzeAudio(f);
      else info = await analyzeFile(f);
      const rec = {
        id: uid(), key, name: f.name, rel, kind, type: f.type || '',
        size: f.size, w: info.w, h: info.h, dur: info.dur || 0,
        mtime: f.lastModified || Date.now(), added: Date.now(),
        cat: info.auto.cat, autoCat: info.auto.cat, conf: info.auto.conf,
        persons: [], tags: [], fav: false, rating: 0,
        thumb: info.thumb, blob: f
      };
      await dbPut('photos', rec);
      S.photos.push(rec);
      added++;
    } catch(e){ failed++; }

    if(i % 6 === 0) await tick(8);
  }

  $('pBar').style.width = '100%'; $('pPct').textContent = '100%';
  $('pCount').textContent = `${files.length} / ${files.length}`;
  $('pName').textContent = '完成';
  await tick(320);
  $('progress').classList.remove('on');
  iPad = false;
  renderAll();
  updateStorage();
  toast(`已导入 ${added} 项` + (dup ? `，跳过重复 ${dup} 项` : '') + (failed ? `，失败 ${failed} 项` : ''));
}

/* 拖入文件夹：递归展开 */
async function collectEntry(entry, out, path){
  if(!entry) return;
  if(entry.isFile){
    await new Promise(res => {
      entry.file(f => {
        try { Object.defineProperty(f, 'webkitRelativePath', { value: path + f.name, configurable:true }); } catch(e){}
        out.push(f); res();
      }, () => res());
    });
  } else if(entry.isDirectory){
    const reader = entry.createReader();
    const read = () => new Promise(res => reader.readEntries(es => res(es), () => res([])));
    const sub = path + entry.name + '/';
    let batch;
    while((batch = await read()).length){
      for(const e of batch) await collectEntry(e, out, sub);
    }
  }
}

/* ---------- 视图数据 ---------- */
function matchSearch(p, q){
  if(!q) return true;
  const hay = [p.name, p.rel, ...(p.tags||[]), ...(p.persons||[]), (CATS[p.cat]||CATS.other).label,
    p.kind === 'video' ? '视频' : p.kind === 'audio' ? '音频' : '图片'].join(' ').toLowerCase();
  return hay.includes(q.toLowerCase());
}
function currentList(){
  let list = S.photos.slice();
  if(S.view === 'fav') list = list.filter(p => p.fav);
  else if(S.view === 'video') list = list.filter(p => p.kind === 'video');
  else if(S.view === 'audio') list = list.filter(p => p.kind === 'audio');
  else if(S.view === 'recent'){
    const week = Date.now() - 7 * 864e5;
    const r = list.filter(p => p.added > week);
    list = (r.length ? r : list.slice().sort((a,b)=>b.added-a.added).slice(0,60));
  }
  else if(S.view.startsWith('cat:')) list = list.filter(p => p.cat === S.view.slice(4));
  else if(S.view === 'album'){
    const a = S.albums.find(x => x.id === S.albumId);
    const ids = new Set(a ? a.photoIds : []);
    list = list.filter(p => ids.has(p.id));
  }
  if(S.catFilter && S.view === 'all') list = list.filter(p => p.cat === S.catFilter);
  if(S.personFilter) list = list.filter(p => (p.persons||[]).includes(S.personFilter));
  list = list.filter(p => matchSearch(p, S.search));

  const by = {
    added_desc:(a,b)=>b.added-a.added, added_asc:(a,b)=>a.added-b.added,
    name_asc:(a,b)=>a.name.localeCompare(b.name,'zh'),
    size_desc:(a,b)=>b.size-a.size, mtime_desc:(a,b)=>b.mtime-a.mtime
  }[S.sort] || ((a,b)=>b.added-a.added);
  return list.sort(by);
}
function allPersons(){
  const m = new Map();
  S.photos.forEach(p => (p.persons||[]).forEach(n => m.set(n, (m.get(n)||0)+1)));
  return [...m.entries()].sort((a,b)=>b[1]-a[1]);
}

/* ---------- 标题与计数 ---------- */
function viewLabel(){
  if(S.search) return '搜索结果';
  if(S.view === 'all') return '全部照片';
  if(S.view === 'recent') return '最近导入';
  if(S.view === 'fav') return '收藏';
  if(S.view === 'video') return '视频';
  if(S.view === 'audio') return '音频';
  if(S.view.startsWith('cat:')) return CATS[S.view.slice(4)].label;
  if(S.view === 'album'){
    const a = S.albums.find(x => x.id === S.albumId);
    return a ? a.name : '相册';
  }
  return '全部照片';
}
function updateCounts(){
  $('cAll').textContent = S.photos.length;
  const week = Date.now() - 7 * 864e5;
  const rc = S.photos.filter(p => p.added > week).length;
  $('cRecent').textContent = rc || Math.min(60, S.photos.length);
  $('cFav').textContent = S.photos.filter(p => p.fav).length;
  const vc = $('cVideo'), ac = $('cAudio');
  if(vc) vc.textContent = S.photos.filter(p => p.kind === 'video').length;
  if(ac) ac.textContent = S.photos.filter(p => p.kind === 'audio').length;
  CAT_KEYS.forEach(k => {
    const el = document.querySelector(`.cnt[data-count="${k}"]`);
    if(el) el.textContent = S.photos.filter(p => p.cat === k).length;
  });
  document.querySelectorAll('.nav-item').forEach(el => {
    const v = el.dataset.view;
    let on = false;
    if(v === S.view && v !== 'album') on = true;
    el.setAttribute('aria-current', on ? 'true' : 'false');
  });
  document.querySelectorAll('.nav-item[data-album]').forEach(el => {
    el.setAttribute('aria-current', (S.view === 'album' && el.dataset.album === S.albumId) ? 'true' : 'false');
  });
}
function updateStorage(){
  const total = S.photos.reduce((s,p)=>s+(p.size||0),0);
  const nv = S.photos.filter(p=>p.kind==='video').length, na = S.photos.filter(p=>p.kind==='audio').length;
  $('storeText').textContent = `${S.photos.length} 项 · ${fmtSize(total)}`;
  $('storeBar').style.width = Math.min(100, S.photos.length / 2000 * 100) + '%';
  $('statusSize').textContent = fmtSize(total);
  $('statusCount').textContent = `${S.photos.length} 项` + (nv ? ` · 视频 ${nv}` : '') + (na ? ` · 音频 ${na}` : '');
}
function renderAlbums(){
  const box = $('albumList');
  if(!S.albums.length){
    box.innerHTML = `<div class="nav-sub"><span class="dot"></span>还没有相册</div>`;
    return;
  }
  box.innerHTML = S.albums.map(a => `
    <button class="nav-item" data-album="${a.id}" data-view="album:${a.id}">
      <svg class="ico"><use href="#i-album" xlink:href="#i-album"/></svg>
      <span class="txt">${esc(a.name)}</span><span class="cnt">${a.photoIds.length}</span>
    </button>`).join('');
}

/* ---------- 筛选条 ---------- */
function renderSubbar(){
  const bar = $('subbar');
  let html = '';
  if(S.search){
    html += `<span class="chip" aria-pressed="true">搜索：${esc(S.search)}</span>
             <button class="chip" id="clearSearch">清除搜索</button>`;
  } else if(S.view === 'all'){
    html += `<button class="chip" ${S.catFilter ? '' : 'aria-pressed="true"'} data-cat="">全部 <span class="n">${S.photos.length}</span></button>`;
    html += CAT_KEYS.map(k => `<button class="chip" ${S.catFilter === k ? 'aria-pressed="true"' : ''} data-cat="${k}">${CATS[k].label} <span class="n">${S.photos.filter(p=>p.cat===k).length}</span></button>`).join('');
  } else if(S.view === 'cat:person'){
    const ps = allPersons();
    if(ps.length){
      html += `<button class="chip" ${S.personFilter ? '' : 'aria-pressed="true"'} data-person="">全部人物</button>`;
      html += ps.slice(0,14).map(([n,c]) => `<button class="chip" ${S.personFilter===n?'aria-pressed="true"':''} data-person="${esc(n)}">${esc(n)} <span class="n">${c}</span></button>`).join('');
    } else {
      html += `<span class="chip" style="color:var(--text-3);background:transparent">尚未命名人物 · 在照片详情里添加姓名即可按人查找</span>`;
    }
  } else if(S.view === 'album'){
    html += `<span class="chip" aria-pressed="true">相册内 ${currentList().length} 张</span>
             <button class="chip" id="editAlbum" style="background:transparent;border-color:var(--line)">重命名</button>`;
  } else if(S.view === 'recent'){
    html += `<span class="chip" aria-pressed="true">最近 7 天导入</span>`;
  } else if(S.view === 'fav'){
    html += `<span class="chip" aria-pressed="true">已收藏 ${S.photos.filter(p=>p.fav).length} 张</span>`;
  }
  bar.innerHTML = html + `<div class="spacer"></div>`;
  const cs = $('clearSearch'); if(cs) cs.onclick = () => { S.search = ''; $('searchInput').value = ''; renderAll(); };
  bar.querySelectorAll('[data-cat]').forEach(c => c.onclick = () => { S.catFilter = c.dataset.cat || null; renderAll(); });
  bar.querySelectorAll('[data-person]').forEach(c => c.onclick = () => { S.personFilter = c.dataset.person || null; renderAll(); });
  const ea = $('editAlbum'); if(ea) ea.onclick = () => renameAlbum(S.albumId);
}

/* ---------- 空状态 ---------- */
function emptyHTML(){
  return `<div class="empty">
    <div class="empty-frame" id="dropFrame">
      <span class="corner c1"></span><span class="corner c2"></span><span class="corner c3"></span><span class="corner c4"></span>
      <div class="inner">
        <svg class="empty-ico"><use href="#i-image" xlink:href="#i-image"/></svg>
        <h2>把照片和视频放进来</h2>
        <p>选择文件夹或单个文件导入，支持图片、视频、音频。只有导入过的内容才会进入 CC 图库管理，未导入的文件不会被扫描或改动。</p>
        <div class="empty-actions">
          <button class="btn" id="emptyDir"><svg><use href="#i-folder" xlink:href="#i-folder"/></svg>导入文件夹</button>
          <button class="btn ghost" id="emptyFile"><svg><use href="#i-file" xlink:href="#i-file"/></svg>选择文件</button>
        </div>
      </div>
    </div>
    <div class="empty-tip">
      <span>图片 JPG / PNG / WebP / GIF / BMP</span>
      <span>视频 MP4 / MOV / WebM / MKV · 音频 MP3 / WAV / FLAC / M4A</span>
      <span>数据保存在 <b>本机</b></span>
    </div>
  </div>`;
}
function bindEmpty(){
  const d = $('emptyDir'), f = $('emptyFile');
  if(d) d.onclick = () => $('dirInput').click();
  if(f) f.onclick = () => $('fileInput').click();
}

/* ---------- 照片网格 ---------- */
function calcCols(){
  const gap = S.density === 'sm' ? 10 : S.density === 'lg' ? 12 : 10;
  const target = S.density === 'sm' ? 128 : S.density === 'lg' ? 248 : 176;
  const w = ($('content').clientWidth || 900) - 40;
  return Math.max(2, Math.floor((w + gap) / (target + gap)));
}
function renderGrid(){
  const box = $('contentInner');
  const list = currentList();

  if(!S.photos.length){
    box.innerHTML = emptyHTML(); bindEmpty(); return;
  }
  if(!list.length){
    box.innerHTML = `<div class="hollow">
      <svg><use href="#i-search" xlink:href="#i-search"/></svg>
      <p>当前条件下没有照片</p>
      <button class="btn ghost sm" id="resetFilter">清除筛选条件</button>
    </div>`;
    const r = $('resetFilter');
    if(r) r.onclick = () => { S.search=''; S.catFilter=null; S.personFilter=null; $('searchInput').value=''; renderAll(); };
    return;
  }

  let cols = calcCols();
  // 避免最后一行只剩 1 个
  if(cols > 2 && list.length > cols && list.length % cols === 1) cols -= 1;
  box.innerHTML = `<div class="grid ${S.density==='sm'?'dense':''}" style="--cols:${cols}">
    ${list.map(p => {
      const cat = CATS[p.cat] || CATS.other;
      const on = S.selected.has(p.id);
      const isVid = p.kind === 'video', isAud = p.kind === 'audio';
      const tagTxt = isVid ? `视频 ${fmtDur(p.dur)}` : isAud ? `音频 ${fmtDur(p.dur)}` : cat.label;
      const subTxt = isAud ? `${fmtDur(p.dur)} · ${fmtSize(p.size)}`
        : (p.w ? `${p.w}×${p.h} · ${fmtSize(p.size)}` : `${fmtSize(p.size)}`);
      return `<figure class="tile ${on?'sel':''}" data-id="${p.id}" title="${esc(p.name)}">
        ${S.selectMode ? `<span class="check"><svg><use href="#i-check" xlink:href="#i-check"/></svg></span>` : `<span class="check"><svg><use href="#i-check" xlink:href="#i-check"/></svg></span>`}
        <div class="badge"><span class="cat">${tagTxt}</span></div>
        ${p.fav ? `<span class="fav"><svg><use href="#i-star-fill" xlink:href="#i-star-fill"/></svg></span>` : ''}
        ${isVid ? `<div class="play"><svg><use href="#i-play" xlink:href="#i-play"/></svg></div>` : ''}
        <img src="${p.thumb}" alt="${esc(p.name)}" loading="lazy">
        <div class="meta"><b>${esc(p.name)}</b><span>${subTxt}</span></div>
      </figure>`;
    }).join('')}
  </div>`;
}

/* ---------- 渲染入口 ---------- */
function renderAll(){
  updateCounts();
  updateStorage();
  renderAlbums();
  const list = currentList();
  $('viewTitle').textContent = viewLabel();
  let meta = `${list.length} 项`;
  if(S.search) meta += ` · 关键词「${S.search}」`;
  if(S.personFilter) meta += ` · ${S.personFilter}`;
  $('viewMeta').textContent = meta;
  $('statusFilter').textContent = (S.search || S.catFilter || S.personFilter) ? '已筛选' : '无筛选';
  renderSubbar();
  renderGrid();
  $('selCount').textContent = S.selected.size;
  $('selbar').classList.toggle('on', S.selectMode && S.selected.size > 0);
  if(S.detailId){
    const p = S.photos.find(x => x.id === S.detailId);
    if(p) renderDetail(p); else closeDrawer();
  }
}

/* ---------- 详情抽屉 ---------- */
function openDetail(id){
  S.detailId = id;
  const p = S.photos.find(x => x.id === id);
  if(!p) return;
  $('drawer').classList.add('on');
  $('drawer').setAttribute('aria-hidden','false');
  document.querySelector('.app').classList.add('withdrawer');
  renderDetail(p);
  clearTimeout(window._dt);
  window._dt = setTimeout(() => { if(S.detailId) renderGrid(); }, 360);
}
function closeDrawer(){
  S.detailId = null;
  $('drawer').classList.remove('on');
  $('drawer').setAttribute('aria-hidden','true');
  document.querySelector('.app').classList.remove('withdrawer');
  clearTimeout(window._dt);
  window._dt = setTimeout(renderGrid, 360);
}
function renderPreview(p){
  const box = $('dPreview');
  const kind = p.kind || 'image';
  const url = photoUrl(p);
  if(kind === 'video'){
    box.innerHTML = `<video id="dMediaEl" controls playsinline preload="metadata" src="${url}"></video>`;
  } else if(kind === 'audio'){
    box.innerHTML = `<div class="audio-box"><div class="wave" style="background-image:url(${p.thumb})"></div><audio id="dMediaEl" controls src="${url}"></audio></div>`;
  } else {
    box.innerHTML = `<img id="dImg" src="${url}" alt="">`;
  }
}
function renderDetail(p){
  $('dTitle').textContent = p.name;
  const kind = p.kind || 'image';
  renderPreview(p);
  $('dExport').style.display = kind === 'image' ? '' : 'none';
  const cat = CATS[p.cat] ? p.cat : 'other';
  const autoTxt = (p.conf && CATS[p.autoCat]) ? `${CATS[p.autoCat].label} · ${Math.round(p.conf*100)}%` : '—';

  const catBlock = kind === 'image' ? `
    <div class="field">
      <label>分区 <span class="mini">可手动校正</span></label>
      <div class="cat-row">
        ${CAT_KEYS.map(k => `<button class="chip" data-setcat="${k}" ${cat===k?'aria-pressed="true"':''}>${CATS[k].label}</button>`).join('')}
      </div>
      <div style="margin-top:8px;font-size:11px;color:var(--text-3)">自动识别：${autoTxt}</div>
    </div>

    <div class="field">
      <label>人物 <span class="mini">用于按人查找</span></label>
      <div class="person-row" id="personRow">
        ${(p.persons||[]).map(n => `<span class="ptag">${esc(n)}<button data-delperson="${esc(n)}"><svg><use href="#i-close" xlink:href="#i-close"/></svg></button></span>`).join('')}
        <input class="inline-input" id="personInput" placeholder="输入姓名后回车">
      </div>
    </div>` : `
    <div class="field">
      <label>媒体类型</label>
      <div style="font-size:12.5px;color:var(--text-2)">${kind === 'video' ? '视频' : '音频'}${p.dur ? ` · 时长 ${fmtDur(p.dur)}` : ''}</div>
    </div>`;

  $('dBody').innerHTML = `
    ${catBlock}

    <div class="field">
      <label>标签 <span class="mini">逗号分隔</span></label>
      <div class="person-row" id="tagRow">
        ${(p.tags||[]).map(n => `<span class="ptag">${esc(n)}<button data-deltag="${esc(n)}"><svg><use href="#i-close" xlink:href="#i-close"/></svg></button></span>`).join('')}
        <input class="inline-input" id="tagInput" placeholder="添加标签">
      </div>
    </div>

    <div class="field" style="display:flex;align-items:center;justify-content:space-between">
      <label style="margin:0">评分</label>
      <div class="stars" id="stars">
        ${[1,2,3,4,5].map(i => `<button data-star="${i}" class="${p.rating>=i?'on':''}"><svg><use href="${p.rating>=i?'i-star-fill':'i-star'}" xlink:href="${p.rating>=i?'i-star-fill':'i-star'}"/></svg></button>`).join('')}
      </div>
    </div>

    <div class="field">
      <label>操作</label>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="chip" id="toggleFav" ${p.fav?'aria-pressed="true"':''}><svg style="width:13px;height:13px"><use href="#i-star" xlink:href="#i-star"/></svg>${p.fav?'已收藏':'收藏'}</button>
        <button class="chip" id="addAlbum"><svg style="width:13px;height:13px"><use href="#i-album" xlink:href="#i-album"/></svg>加入相册</button>
      </div>
    </div>

    <div class="field">
      <label>文件信息</label>
      <dl class="meta-list">
        <div><dt>${kind === 'audio' ? '时长' : '尺寸'}</dt><dd>${kind === 'audio' ? fmtDur(p.dur) : (p.w ? `${p.w} × ${p.h}` : '—')}</dd></div>
        ${kind === 'video' ? `<div><dt>时长</dt><dd>${fmtDur(p.dur)}</dd></div>` : ''}
        <div><dt>大小</dt><dd>${fmtSize(p.size)}</dd></div>
        <div><dt>格式</dt><dd>${esc(((p.name||'').split('.').pop() || (p.type||'').split('/').pop() || '').toUpperCase() || '—')}</dd></div>
        <div><dt>拍摄时间</dt><dd>${fmtDate(p.mtime)}</dd></div>
        <div><dt>导入时间</dt><dd>${fmtDate(p.added)}</dd></div>
        <div><dt>来源</dt><dd title="${esc(p.rel)}">${esc(p.rel)}</dd></div>
      </dl>
    </div>`;

  $('dBody').querySelectorAll('[data-setcat]').forEach(b => b.onclick = async () => {
    p.cat = b.dataset.setcat;
    await dbPut('photos', p);
    renderAll();
    toast(`已归入「${CATS[p.cat].label}」`);
  });
  $('dBody').querySelectorAll('[data-delperson]').forEach(b => b.onclick = async () => {
    p.persons = (p.persons||[]).filter(n => n !== b.dataset.delperson);
    await dbPut('photos', p); renderAll();
  });
  $('dBody').querySelectorAll('[data-deltag]').forEach(b => b.onclick = async () => {
    p.tags = (p.tags||[]).filter(n => n !== b.dataset.deltag);
    await dbPut('photos', p); renderAll();
  });
  const pi = $('personInput');
  if(pi) pi.addEventListener('keydown', async e => {
    if(e.key !== 'Enter') return;
    const v = pi.value.trim(); if(!v) return;
    p.persons = [...new Set([...(p.persons||[]), v])];
    await dbPut('photos', p); renderAll();
  });
  const ti = $('tagInput');
  ti.addEventListener('keydown', async e => {
    if(e.key !== 'Enter') return;
    const vs = ti.value.split(/[,，]/).map(s=>s.trim()).filter(Boolean);
    if(!vs.length) return;
    p.tags = [...new Set([...(p.tags||[]), ...vs])];
    await dbPut('photos', p); renderAll();
  });
  $('stars') && $('stars').querySelectorAll('[data-star]').forEach(b => b.onclick = async () => {
    const n = +b.dataset.star;
    p.rating = p.rating === n ? 0 : n;
    await dbPut('photos', p); renderAll();
  });
  $('toggleFav').onclick = async () => { p.fav = !p.fav; await dbPut('photos', p); renderAll(); if($('viewer').classList.contains('on')) syncViewerFav(); };
  $('addAlbum').onclick = () => pickAlbum([p.id]);
}

/* ---------- 全屏查看 ---------- */
let viewerList = [];
function openViewer(id){
  viewerList = currentList();
  const i = viewerList.findIndex(p => p.id === id);
  S.viewerIdx = i < 0 ? 0 : i;
  $('viewer').classList.add('on');
  showViewer();
}
function showViewer(){
  const p = viewerList[S.viewerIdx];
  if(!p) return;
  const kind = p.kind || 'image';
  const url = photoUrl(p);
  const img = $('vImg'), vid = $('vVid'), audBox = $('vAudio');
  img.style.display = kind === 'image' ? '' : 'none';
  img.classList.remove('zoom');
  vid.style.display = kind === 'video' ? 'block' : 'none';
  audBox.style.display = kind === 'audio' ? 'flex' : 'none';
  if(kind === 'video'){ vid.poster = p.thumb || ''; vid.src = url; }
  else { try{ vid.pause(); }catch(e){} vid.removeAttribute('src'); vid.load(); }
  if(kind === 'audio'){ $('vAudImg').src = p.thumb || ''; $('vAud').src = url; }
  else { const a = $('vAud'); try{ a.pause(); }catch(e){} a.removeAttribute('src'); }
  if(kind === 'image') img.src = url;
  $('vName').textContent = p.name;
  $('vIdx').textContent = `${S.viewerIdx+1} / ${viewerList.length}`;
  $('vDim').textContent = kind === 'image' ? `${p.w} × ${p.h}` : `${kind === 'video' ? '视频' : '音频'} · ${fmtDur(p.dur)}`;
  $('vStrip').innerHTML = viewerList.slice(Math.max(0,S.viewerIdx-8), S.viewerIdx+9)
    .map((q, k) => {
      const realIdx = Math.max(0,S.viewerIdx-8) + k;
      return `<img src="${q.thumb}" data-jump="${realIdx}" class="${realIdx===S.viewerIdx?'on':''}" alt="">`;
    }).join('');
  $('vStrip').querySelectorAll('[data-jump]').forEach(el => el.onclick = () => { S.viewerIdx = +el.dataset.jump; showViewer(); });
  syncViewerFav();
}
function syncViewerFav(){
  const p = viewerList[S.viewerIdx]; if(!p) return;
  const icon = p.fav ? '#i-star-fill' : '#i-star';
  $('vFav').querySelector('use').setAttribute('href', icon);
  $('vFav').querySelector('use').setAttribute('xlink:href', icon);
}
function stepViewer(d){
  if(!viewerList.length) return;
  S.viewerIdx = (S.viewerIdx + d + viewerList.length) % viewerList.length;
  showViewer();
}
function closeViewer(){ $('viewer').classList.remove('on'); }

/* ---------- 浮层菜单 ---------- */
function showPop(anchor, items){
  const pop = $('pop');
  pop.innerHTML = items.map((it, i) => it.sep ? `<div class="sep"></div>` :
    `<button data-i="${i}" class="${it.on?'on':''}">${it.icon?`<svg><use href="#${it.icon}" xlink:href="#${it.icon}"/></svg>`:''}${it.label}</button>`).join('');
  pop.classList.add('on');
  const r = anchor.getBoundingClientRect();
  const pw = pop.offsetWidth, ph = pop.offsetHeight;
  let x = r.right - pw, y = r.bottom + 6;
  if(x < 8) x = 8;
  if(y + ph > innerHeight - 8) y = r.top - ph - 6;
  pop.style.left = x + 'px'; pop.style.top = y + 'px';
  pop.querySelectorAll('button').forEach(b => b.onclick = () => {
    const it = items[+b.dataset.i]; hidePop();
    if(it && it.fn) it.fn();
  });
}
function hidePop(){ $('pop').classList.remove('on'); }

/* ---------- 弹窗 ---------- */
function openModal(html, wide){
  $('modalCard').className = 'modal-card' + (wide ? ' wide' : '');
  $('modalCard').innerHTML = html;
  $('modal').classList.add('on');
}
function closeModal(){ $('modal').classList.remove('on'); }

/* ---------- 相册 ---------- */
function createAlbum(name){
  const a = { id: uid(), name: name || '未命名相册', created: Date.now(), photoIds: [] };
  S.albums.push(a);
  dbPut('albums', a);
  renderAll();
  return a;
}
function newAlbumDialog(){
  openModal(`<h3>新建相册</h3><p>把照片归入自定义相册，便于按主题分区。</p>
    <input type="text" id="albumName" placeholder="例如：2026 沈阳 · 冬" maxlength="24">
    <div class="modal-actions">
      <button class="btn ghost sm" id="mCancel">取消</button>
      <button class="btn sm" id="mOk">创建</button>
    </div>`);
  const inp = $('albumName');
  setTimeout(()=>inp.focus(), 60);
  $('mCancel').onclick = closeModal;
  $('mOk').onclick = () => {
    const v = inp.value.trim(); if(!v){ inp.focus(); return; }
    const a = createAlbum(v); closeModal(); S.view = 'album'; S.albumId = a.id; renderAll(); toast('相册已创建');
  };
  inp.addEventListener('keydown', e => { if(e.key === 'Enter') $('mOk').click(); });
}
function renameAlbum(id){
  const a = S.albums.find(x => x.id === id); if(!a) return;
  openModal(`<h3>重命名相册</h3><p>当前名称：${esc(a.name)}</p>
    <input type="text" id="albumName" value="${esc(a.name)}" maxlength="24">
    <div class="modal-actions">
      <button class="btn ghost sm" id="mCancel">取消</button>
      <button class="btn sm" id="mOk">保存</button>
    </div>`);
  const inp = $('albumName'); setTimeout(()=>inp.focus(),60);
  $('mCancel').onclick = closeModal;
  $('mOk').onclick = async () => {
    const v = inp.value.trim(); if(!v) return;
    a.name = v; await dbPut('albums', a); closeModal(); renderAll(); toast('已重命名');
  };
}
function pickAlbum(ids){
  if(!S.albums.length){
    openModal(`<h3>还没有相册</h3><p>先创建一个相册，再把这些照片放进去。</p>
      <div class="modal-actions"><button class="btn ghost sm" id="mCancel">取消</button>
      <button class="btn sm" id="mNew">新建相册</button></div>`);
    $('mCancel').onclick = closeModal;
    $('mNew').onclick = () => { closeModal(); newAlbumDialog(); };
    return;
  }
  openModal(`<h3>加入相册</h3><p>选择目标相册，${ids.length} 张照片会被加入。</p>
    <div class="tall" id="albumPick">
      ${S.albums.map(a => `<button data-a="${a.id}"><svg><use href="#i-album" xlink:href="#i-album"/></svg>${esc(a.name)} <span style="margin-left:auto;color:var(--text-3);font-family:var(--mono);font-size:11px">${a.photoIds.length}</span></button>`).join('')}
    </div>
    <div class="modal-actions">
      <button class="btn ghost sm" id="mCancel">取消</button>
      <button class="btn ghost sm" id="mNew">新建相册</button>
    </div>`);
  $('mCancel').onclick = closeModal;
  $('mNew').onclick = () => { closeModal(); newAlbumDialog(); };
  $('albumPick').querySelectorAll('[data-a]').forEach(b => b.onclick = async () => {
    const a = S.albums.find(x => x.id === b.dataset.a);
    a.photoIds = [...new Set([...a.photoIds, ...ids])];
    await dbPut('albums', a); closeModal(); renderAll();
    toast(`已加入「${a.name}」`);
  });
}

/* ---------- 移出图库 ---------- */
function confirmRemove(ids){
  openModal(`<h3>移出图库？</h3><p>将从 CC 图库中移除 ${ids.length} 张照片，原文件在磁盘上不受影响。此操作不可撤销。</p>
    <div class="modal-actions">
      <button class="btn ghost sm" id="mCancel">取消</button>
      <button class="btn sm" id="mOk">移出</button>
    </div>`);
  $('mCancel').onclick = closeModal;
  $('mOk').onclick = async () => {
    for(const id of ids){
      const p = S.photos.find(x => x.id === id);
      await dbDel('photos', id);
      dropUrl(id);
      S.photos = S.photos.filter(x => x.id !== id);
      if(p) S.albums.forEach(a => { if(a.photoIds.includes(id)){ a.photoIds = a.photoIds.filter(x => x !== id); dbPut('albums', a); } });
      S.selected.delete(id);
    }
    closeModal(); closeDrawer(); renderAll();
    toast(`已移出 ${ids.length} 张`);
  };
}

/* ---------- 主题 ---------- */
function setTheme(t){
  document.documentElement.dataset.theme = t;
  localStorage.setItem('lumen-theme', t);
  const u = $('themeBtn').querySelector('use');
  const icon = t === 'dark' ? '#i-sun' : '#i-moon';
  u.setAttribute('href', icon);
  u.setAttribute('xlink:href', icon);
}

/* ---------- 导出与转换 ---------- */
const EXT_MAP = { 'image/jpeg':'jpg', 'image/png':'png', 'image/webp':'webp' };
let CV = { format:'keep', quality:90, edge:0, naming:'orig', prefix:'CC' };

function convertTargets(){
  if(S.selected.size) return [...S.selected].map(id => S.photos.find(p => p.id === id)).filter(Boolean);
  return currentList();
}
function safeName(s){
  return (s || 'photo').replace(/[\\/:*?"<>|\n]/g, '_').replace(/\s+/g,' ').trim().slice(0, 60) || 'photo';
}
function exportName(p, o, type, idx){
  const ext = EXT_MAP[type] || 'jpg';
  const rawExt = (p.name.match(/\.[^.]+$/) || [''])[0].toLowerCase();
  const keepExt = o.format === 'keep' && !(o.edge && Math.max(p.w, p.h) > o.edge) ? (rawExt || '.' + ext) : '.' + ext;
  let base = p.name.replace(/\.[^.]+$/, '');
  base = safeName(base);
  if(o.naming === 'seq') base += '_' + String(idx + 1).padStart(3, '0');
  if(o.naming === 'prefix') base = safeName(o.prefix) + '_' + String(idx + 1).padStart(3, '0');
  return base + keepExt;
}

async function encodePhoto(p, o){
  const bmp = await loadBitmap(p.blob);
  const ow = bmp.width || bmp.naturalWidth, oh = bmp.height || bmp.naturalHeight;
  const long = Math.max(ow, oh);
  const scale = (o.edge && long > o.edge) ? o.edge / long : 1;
  const type = o.format === 'keep'
    ? (/^image\/(jpeg|png|webp)$/.test(p.type || '') ? p.type : 'image/jpeg')
    : o.format;

  // 不需要转码时直接复制原始文件
  if(o.format === 'keep' && scale === 1){
    if(bmp.close) bmp.close();
    return { blob: p.blob, type: p.type || 'image/jpeg' };
  }

  const w = Math.max(1, Math.round(ow * scale)), h = Math.max(1, Math.round(oh * scale));
  const c = document.createElement('canvas');
  c.width = w; c.height = h;
  const ctx = c.getContext('2d');
  ctx.imageSmoothingEnabled = true;
  ctx.imageSmoothingQuality = 'high';
  if(type === 'image/jpeg'){ ctx.fillStyle = '#FFFFFF'; ctx.fillRect(0, 0, w, h); }
  ctx.drawImage(bmp, 0, 0, w, h);
  if(bmp.close) bmp.close();

  const blob = await new Promise(r => c.toBlob(r, type, o.quality / 100));
  if(!blob) throw new Error('编码失败');
  return { blob, type };
}

function downloadBlob(blob, name){
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = name;
  document.body.appendChild(a); a.click(); a.remove();
  setTimeout(() => URL.revokeObjectURL(url), 5000);
}

async function runExport(list, opts, useDir, ui){
  ui.dir.disabled = true; ui.dl.disabled = true; ui.cancel.disabled = true;
  ui.status.classList.add('on');
  ui.bar.style.width = '0%';
  let dir = null, ok = 0, fail = 0;
  const used = new Set();

  if(useDir){
    try {
      dir = await window.showDirectoryPicker({ mode:'readwrite' });
    } catch(err){
      if(err && err.name === 'AbortError'){
        ui.dir.disabled = ui.dl.disabled = ui.cancel.disabled = false;
        ui.status.classList.remove('on');
        return;
      }
      toast('无法写入文件夹，已改为逐张下载');
      useDir = false;
    }
  }

  for(let i = 0; i < list.length; i++){
    const p = list[i];
    ui.info.textContent = `${i+1} / ${list.length} · ${p.name}`;
    ui.bar.style.width = Math.round(i / list.length * 100) + '%';
    try {
      const out = await encodePhoto(p, opts);
      let name = exportName(p, opts, out.type, i);
      if(used.has(name)){
        const ext = (name.match(/\.[^.]+$/) || [''])[0];
        name = name.slice(0, name.length - ext.length) + '_' + (used.size + 1) + ext;
      }
      used.add(name);
      if(dir){
        const fh = await dir.getFileHandle(name, { create:true });
        const wr = await fh.createWritable();
        await wr.write(out.blob);
        await wr.close();
      } else {
        downloadBlob(out.blob, name);
        await tick(70);
      }
      ok++;
    } catch(e){
      fail++;
    }
  }

  ui.bar.style.width = '100%';
  ui.info.textContent = `完成 · 成功 ${ok} 张${fail ? `，失败 ${fail} 张` : ''}`;
  ui.dir.disabled = ui.dl.disabled = ui.cancel.disabled = false;
  toast(`已导出 ${ok} 张${fail ? `（失败 ${fail}）` : ''}`);
}

function openConvert(listArg){
  const raw = listArg && listArg.length ? listArg : convertTargets();
  const list = raw.filter(p => (p.kind || 'image') === 'image');
  if(!list.length){ toast('导出与转换只支持图片'); return; }
  CV = { format:'keep', quality:90, edge:0, naming:'orig', prefix:'CC' };

  openModal(`
    <h3>导出与转换</h3>
    <p>${list.length} 张 · 只读取库内副本，原图不受影响</p>

    <div class="cv-row"><label>预设</label><div class="grow" id="cvPreset">
      <button class="chip sm" data-preset="orig">原图直出</button>
      <button class="chip sm" data-preset="share">分享 1920 / 85%</button>
      <button class="chip sm" data-preset="web">网页 1280 / 75%</button>
    </div></div>

    <div class="cv-row"><label>格式</label><div class="grow" id="cvFmt">
      <button class="chip sm" data-fmt="keep">原格式</button>
      <button class="chip sm" data-fmt="image/jpeg">JPG</button>
      <button class="chip sm" data-fmt="image/png">PNG</button>
      <button class="chip sm" data-fmt="image/webp">WebP</button>
    </div></div>

    <div class="cv-row"><label>质量</label><div class="grow">
      <input type="range" id="cvQ" min="40" max="100" value="90">
      <span class="range-val" id="cvQV">90</span>
    </div></div>

    <div class="cv-row"><label>最长边</label><div class="grow">
      <select class="cv-select" id="cvEdge">
        <option value="0">保持原始</option>
        <option value="2560">2560 px</option>
        <option value="1920">1920 px</option>
        <option value="1280">1280 px</option>
        <option value="800">800 px</option>
      </select>
    </div></div>

    <div class="cv-row"><label>命名</label><div class="grow">
      <select class="cv-select" id="cvName">
        <option value="orig">沿用原文件名</option>
        <option value="seq">原文件名 + 序号</option>
        <option value="prefix">统一前缀 + 序号</option>
      </select>
      <input class="inline-input" id="cvPrefix" placeholder="前缀" style="display:none;height:32px;width:120px" value="CC">
    </div></div>

    <div class="cv-hint">JPG / WebP 支持质量压缩；PNG 无损、体积较大。选择文件夹可直接写入磁盘，逐张下载会由浏览器弹出多次下载提示。</div>

    <div class="cv-status" id="cvStatus">
      <div class="cv-track"><i id="cvBar"></i></div>
      <p id="cvInfo">准备中…</p>
    </div>

    <div class="modal-actions">
      <button class="btn ghost sm" id="cvCancel">取消</button>
      <button class="btn ghost sm" id="cvDl">逐张下载</button>
      <button class="btn sm" id="cvDir">选择文件夹导出</button>
    </div>`, true);

  const fmtBtns = $('cvFmt').querySelectorAll('[data-fmt]');
  const presetBtns = $('cvPreset').querySelectorAll('[data-preset]');
  const q = $('cvQ'), qv = $('cvQV'), edge = $('cvEdge'), naming = $('cvName'), prefix = $('cvPrefix');

  const paintFmt = () => fmtBtns.forEach(b => b.setAttribute('aria-pressed', b.dataset.fmt === CV.format ? 'true' : 'false'));
  const paintPreset = () => {
    const hit = { orig:'原图直出', share:'分享 1920 / 85%', web:'网页 1280 / 75%' };
    presetBtns.forEach(b => {
      const map = { orig:[ 'keep',0,90 ], share:[ 'image/jpeg',1920,85 ], web:[ 'image/jpeg',1280,75 ] }[b.dataset.preset];
      b.setAttribute('aria-pressed', (CV.format===map[0] && +edge.value===map[1] && +q.value===map[2]) ? 'true' : 'false');
      if(hit[b.dataset.preset] && b.getAttribute('aria-pressed')==='true') b.dataset.hit = '1';
    });
  };
  const sync = () => { paintFmt(); paintPreset(); };

  fmtBtns.forEach(b => b.onclick = () => { CV.format = b.dataset.fmt; sync(); });
  presetBtns.forEach(b => b.onclick = () => {
    const map = { orig:['keep',0,90], share:['image/jpeg',1920,85], web:['image/jpeg',1280,75] }[b.dataset.preset];
    CV.format = map[0]; edge.value = String(map[1]); q.value = String(map[2]);
    qv.textContent = q.value; sync();
  });
  q.oninput = () => { qv.textContent = q.value; paintPreset(); };
  edge.onchange = () => { paintPreset(); };
  naming.onchange = () => { prefix.style.display = naming.value === 'prefix' ? 'block' : 'none'; };
  $('cvCancel').onclick = closeModal;

  const opts = () => ({ format:CV.format, quality:+q.value, edge:+edge.value, naming:naming.value, prefix:prefix.value });
  const ui = { dir:$('cvDir'), dl:$('cvDl'), cancel:$('cvCancel'), status:$('cvStatus'), bar:$('cvBar'), info:$('cvInfo') };
  $('cvDl').onclick = () => runExport(list, opts(), false, ui);
  $('cvDir').onclick = () => runExport(list, opts(), true, ui);
  sync();
}

/* ---------- 旋转 / 翻转 ---------- */
async function rotatePhoto(p, mode){
  const bmp = await loadBitmap(p.blob);
  const w = bmp.width || bmp.naturalWidth, h = bmp.height || bmp.naturalHeight;
  const swap = mode === 'cw' || mode === 'ccw';
  const cw = swap ? h : w, ch = swap ? w : h;
  const c = document.createElement('canvas');
  c.width = cw; c.height = ch;
  const ctx = c.getContext('2d');
  ctx.save();
  ctx.translate(cw / 2, ch / 2);
  if(mode === 'cw') ctx.rotate(Math.PI / 2);
  else if(mode === 'ccw') ctx.rotate(-Math.PI / 2);
  else if(mode === '180') ctx.rotate(Math.PI);
  else if(mode === 'flip') ctx.scale(-1, 1);
  ctx.drawImage(bmp, -w / 2, -h / 2, w, h);
  ctx.restore();
  if(bmp.close) bmp.close();

  const type = (p.type === 'image/png') ? 'image/png' : 'image/jpeg';
  if(type === 'image/jpeg'){ /* 保留原画面，不做白底填充 */ }
  const blob = await new Promise(r => c.toBlob(r, type, .92));

  const ts = 640;
  const tw = cw >= ch ? Math.min(ts, cw) : Math.round(ts * cw / ch);
  const th = cw >= ch ? Math.round(ts * ch / cw) : Math.min(ts, ch);
  const tc = document.createElement('canvas');
  tc.width = Math.max(1, tw); tc.height = Math.max(1, th);
  tc.getContext('2d').drawImage(c, 0, 0, tc.width, tc.height);
  const thumb = tc.toDataURL('image/jpeg', .78);

  p.blob = blob; p.w = cw; p.h = ch; p.size = blob.size; p.type = type; p.thumb = thumb;
  await dbPut('photos', p);
  dropUrl(p.id);
}

async function rotateSelected(mode){
  const ids = [...S.selected].filter(id => {
    const p = S.photos.find(x => x.id === id);
    return p && (p.kind || 'image') === 'image';
  });
  if(!ids.length){ toast('旋转只作用于图片'); return; }
  for(const id of ids){
    const p = S.photos.find(x => x.id === id);
    if(!p) continue;
    try { await rotatePhoto(p, mode); } catch(e){}
    await tick(20);
  }
  renderAll();
  if($('viewer').classList.contains('on')) showViewer();
  toast(`已处理 ${ids.length} 张`);
}

/* ---------- 视频工具：转格式 / 提取音轨 ---------- */
const VT = { file:null, mode:'video', fmt:'video/mp4', vq:6000000, afmt:'mp3_192', duration:0, w:0, h:0 };

function vBaseName(name, suffix, ext){
  const base = safeName((name || 'video').replace(/\.[^.]+$/, ''));
  return base + suffix + '.' + ext;
}

function openVideoTool(){
  VT.file = null; VT.duration = 0;
  openModal(`
    <h3>视频工具</h3>
    <p>转成 MP4 / WebM，或提取音轨为 MP3 / WAV。文件不离开本机。</p>

    <div class="vid-drop" id="vidDrop">
      <svg class="ico"><use href="#i-film" xlink:href="#i-film"/></svg>
      <div class="info">
        <b id="vidName">拖入或选择视频文件</b>
        <span id="vidMeta">MP4 · MOV · WebM · MKV · AVI</span>
      </div>
      <button class="btn ghost sm" id="vidPick" type="button">选择视频</button>
    </div>

    <div class="cv-row"><label>操作</label><div class="grow" id="vidMode">
      <button class="chip sm" data-mode="video">转格式</button>
      <button class="chip sm" data-mode="audio">提取音频</button>
    </div></div>

    <div class="cv-row" id="vidFmtRow"><label>输出</label><div class="grow" id="vidFmt">
      <button class="chip sm" data-fmt="video/mp4">MP4 · H.264</button>
      <button class="chip sm" data-fmt="video/webm;codecs=vp9,opus">WebM · VP9</button>
    </div></div>

    <div class="cv-row" id="vidQRow"><label>画质</label><div class="grow" id="vidQ">
      <button class="chip sm" data-q="12000000">高 · 12 Mbps</button>
      <button class="chip sm" data-q="6000000">中 · 6 Mbps</button>
      <button class="chip sm" data-q="2500000">省空间 · 2.5 Mbps</button>
    </div></div>

    <div class="cv-row" id="vidAudRow" style="display:none"><label>音频</label><div class="grow" id="vidAud">
      <button class="chip sm" data-a="mp3_192">MP3 · 192 kbps</button>
      <button class="chip sm" data-a="mp3_128">MP3 · 128 kbps</button>
      <button class="chip sm" data-a="wav">WAV · 无损</button>
    </div></div>

    <div class="cv-hint" id="vidHint">转格式按播放速度实时编码，耗时≈视频时长；提取音频为解码处理，通常几秒内完成。</div>

    <div class="cv-status" id="vidStatus">
      <div class="cv-track"><i id="vidBar"></i></div>
      <p id="vidInfo">准备就绪</p>
    </div>

    <div class="modal-actions">
      <button class="btn ghost sm" id="vidCancel">取消</button>
      <button class="btn sm" id="vidRun" disabled>开始处理</button>
    </div>`, true);

  $('vidPick').onclick = e => { e.stopPropagation(); $('videoInput').click(); };
  $('vidDrop').onclick = () => $('videoInput').click();
  ['dragenter','dragover'].forEach(ev => $('vidDrop').addEventListener(ev, e => { e.preventDefault(); $('vidDrop').classList.add('hot'); }));
  ['dragleave','drop'].forEach(ev => $('vidDrop').addEventListener(ev, e => { e.preventDefault(); $('vidDrop').classList.remove('hot'); }));
  $('vidDrop').addEventListener('drop', e => {
    const f = e.dataTransfer.files && e.dataTransfer.files[0];
    if(f) setVideoFile(f);
  });

  $('vidMode').querySelectorAll('[data-mode]').forEach(b => b.onclick = () => {
    VT.mode = b.dataset.mode;
    syncVideoUI();
  });
  $('vidFmt').querySelectorAll('[data-fmt]').forEach(b => b.onclick = () => { VT.fmt = b.dataset.fmt; syncVideoUI(); });
  $('vidQ').querySelectorAll('[data-q]').forEach(b => b.onclick = () => { VT.vq = +b.dataset.q; syncVideoUI(); });
  $('vidAud').querySelectorAll('[data-a]').forEach(b => b.onclick = () => { VT.afmt = b.dataset.a; syncVideoUI(); });
  $('vidCancel').onclick = closeModal;
  $('vidRun').onclick = runVideoTask;
  syncVideoUI();
}

function syncVideoUI(){
  const audio = VT.mode === 'audio';
  $('vidFmtRow').style.display = audio ? 'none' : 'flex';
  $('vidQRow').style.display = audio ? 'none' : 'flex';
  $('vidAudRow').style.display = audio ? 'flex' : 'none';
  $('vidHint').textContent = audio
    ? '提取音频走解码流程，通常几秒完成；输出时长与原视频一致。'
    : (VT.fmt.indexOf('mp4') >= 0
        ? 'MP4 输出 H.264 视频 + Opus 音频，Chrome/Edge 可直接播放；长边限制 1920，实时编码耗时≈视频时长。'
        : 'WebM 输出 VP9 + Opus，浏览器通用；实时编码耗时≈视频时长，转换期间请勿关闭窗口。');
  $('vidMode').querySelectorAll('[data-mode]').forEach(b => b.setAttribute('aria-pressed', b.dataset.mode === VT.mode ? 'true' : 'false'));
  $('vidFmt').querySelectorAll('[data-fmt]').forEach(b => b.setAttribute('aria-pressed', b.dataset.fmt === VT.fmt ? 'true' : 'false'));
  $('vidQ').querySelectorAll('[data-q]').forEach(b => b.setAttribute('aria-pressed', +b.dataset.q === VT.vq ? 'true' : 'false'));
  $('vidAud').querySelectorAll('[data-a]').forEach(b => b.setAttribute('aria-pressed', b.dataset.a === VT.afmt ? 'true' : 'false'));
  $('vidRun').disabled = !VT.file;
}

async function setVideoFile(f){
  if(!f) return;
  if(!/^video\//.test(f.type) && !/\.(mp4|mov|m4v|webm|mkv|avi|mts|ts)$/i.test(f.name)){
    toast('请选择视频文件'); return;
  }
  VT.file = f; VT.duration = 0; VT.w = 0; VT.h = 0;
  $('vidName').textContent = f.name;
  $('vidMeta').textContent = `${fmtSize(f.size)} · 读取信息中…`;
  $('vidInfo').textContent = '准备就绪';
  $('vidBar').style.width = '0%';
  $('vidStatus').classList.remove('on');
  syncVideoUI();

  try {
    const url = URL.createObjectURL(f);
    const v = document.createElement('video');
    v.preload = 'metadata'; v.src = url;
    await new Promise((res, rej) => { v.onloadedmetadata = res; v.onerror = () => rej(new Error('无法解析该视频')); });
    VT.duration = isFinite(v.duration) ? v.duration : 0;
    VT.w = v.videoWidth; VT.h = v.videoHeight;
    URL.revokeObjectURL(url);
    const mm = Math.floor(VT.duration / 60), ss = Math.round(VT.duration % 60);
    $('vidMeta').textContent = `${VT.w}×${VT.h} · ${mm}:${String(ss).padStart(2,'0')} · ${fmtSize(f.size)}`;
    if(VT.duration > 600) toast('视频超过 10 分钟，实时转码会比较久');
  } catch(e){
    $('vidMeta').textContent = `${fmtSize(f.size)} · 无法读取时长（仍可尝试处理）`;
  }
}

async function runVideoTask(){
  if(!VT.file) return;
  const run = $('vidRun'), cancel = $('vidCancel');
  const status = $('vidStatus'), bar = $('vidBar'), info = $('vidInfo');
  run.disabled = true; cancel.disabled = true;
  status.classList.add('on'); bar.style.width = '0%';

  const file = VT.file;
  const audioMode = VT.mode === 'audio';
  info.textContent = audioMode ? '正在解码音轨…' : '正在准备编码器…';

  try {
    let blob, name;
    if(audioMode){
      const ac = new (window.AudioContext || window.webkitAudioContext)();
      // 用户手势内创建，保证可用
      if(ac.state === 'suspended') await ac.resume().catch(()=>{});
      const ab = await file.arrayBuffer();
      info.textContent = '正在解码音轨…';
      const buf = await ac.decodeAudioData(ab);
      const dur = buf.duration;
      if(VT.afmt === 'wav'){
        info.textContent = '正在生成 WAV…';
        bar.style.width = '80%';
        blob = encodeWAV(buf);
        name = vBaseName(file.name, '_audio', 'wav');
      } else {
        const kbps = VT.afmt === 'mp3_192' ? 192 : 128;
        info.textContent = '正在加载 MP3 编码器…';
        const lame = await loadLame();
        info.textContent = '正在编码 MP3…';
        blob = await encodeMP3(buf, kbps, p => {
          bar.style.width = Math.round(p * 100) + '%';
          info.textContent = `正在编码 MP3… ${Math.round(p * 100)}%`;
        });
        name = vBaseName(file.name, '_audio', 'mp3');
      }
      ac.close && ac.close();
      bar.style.width = '100%';
      finishVideoTask(blob, name, info, bar, run, cancel, `${Math.round(dur)} 秒音频`);
    } else {
      const mime = VT.fmt;
      const ext = mime.indexOf('mp4') >= 0 ? 'mp4' : 'webm';
      info.textContent = '正在转码（实时）…';
      let out;
      if(ext === 'mp4'){
        try {
          out = await transcodeH264(file, VT.vq, p => {
            bar.style.width = Math.round(p * 100) + '%';
            info.textContent = `正在转码 ${Math.round(p * 100)}% · 请勿关闭窗口`;
          });
        } catch(e){
          toast('H.264 编码不可用，改用兼容模式');
          out = await transcodeVideo(file, mime, VT.vq, p => {
            bar.style.width = Math.round(p * 100) + '%';
            info.textContent = `正在转码 ${Math.round(p * 100)}% · 请勿关闭窗口`;
          });
        }
      } else {
        out = await transcodeVideo(file, mime, VT.vq, p => {
          bar.style.width = Math.round(p * 100) + '%';
          info.textContent = `正在转码 ${Math.round(p * 100)}% · 请勿关闭窗口`;
        });
      }
      bar.style.width = '100%';
      finishVideoTask(out, vBaseName(file.name, '_converted', ext), info, bar, run, cancel, '视频');
    }
  } catch(e){
    info.textContent = '处理失败：' + (e && e.message ? e.message : '不支持该文件');
    toast('处理失败，可换一个格式再试');
    bar.style.width = '0%';
    run.disabled = false; cancel.disabled = false;
  }
}

function finishVideoTask(blob, name, info, bar, run, cancel, kind){
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = name;
  document.body.appendChild(a); a.click(); a.remove();
  setTimeout(() => URL.revokeObjectURL(url), 8000);
  info.textContent = `完成 · ${name} · ${fmtSize(blob.size)}`;
  toast(`已生成 ${kind}：${name}`);
  run.disabled = false; cancel.disabled = false;
}

/* H.264 转码：WebCodecs 编码 + mp4-muxer 封装（实时） */
let muxerMod = null;
async function loadMuxer(){
  if(muxerMod) return muxerMod;
  muxerMod = await import('https://fastly.jsdelivr.net/npm/mp4-muxer@5.1.5/+esm');
  return muxerMod;
}

async function transcodeH264(file, vbps, onProgress){
  if(!('VideoEncoder' in window) || !('AudioEncoder' in window)) throw new Error('浏览器不支持 WebCodecs');
  const probe = await VideoEncoder.isConfigSupported({ codec:'avc1.42001f', width:640, height:480, bitrate:vbps, framerate:30 });
  if(!probe.supported) throw new Error('不支持 H.264 编码');
  const { Muxer, ArrayBufferTarget } = await loadMuxer();

  const url = URL.createObjectURL(file);
  const v = document.createElement('video');
  v.src = url; v.playsInline = true; v.preload = 'auto'; v.muted = true;
  v.style.cssText = 'position:fixed;left:-9999px;top:0;width:2px;height:2px;opacity:0;pointer-events:none';
  document.body.appendChild(v);
  await new Promise((res, rej) => { v.onloadedmetadata = res; v.onerror = () => rej(new Error('无法解码该视频')); });

  const ow = v.videoWidth, oh = v.videoHeight;
  const scale = Math.min(1, 1920 / Math.max(ow, oh));
  let W = Math.round(ow * scale), H = Math.round(oh * scale);
  W -= W % 2; H -= H % 2;

  // 音轨：解码 + 重采样到 48k
  let res = null, audioCh = 0;
  try {
    const ac = new (window.AudioContext || window.webkitAudioContext)();
    const abuf = await ac.decodeAudioData(await file.arrayBuffer());
    ac.close && ac.close();
    audioCh = Math.min(2, abuf.numberOfChannels);
    const sr = 48000;
    const oc = new OfflineAudioContext(audioCh, Math.max(1, Math.ceil(abuf.duration * sr)), sr);
    const src = oc.createBufferSource();
    src.buffer = abuf; src.connect(oc.destination); src.start();
    res = await oc.startRendering();
  } catch(e){ res = null; }

  const opts = { target:new ArrayBufferTarget(), video:{ codec:'avc', width:W, height:H }, fastStart:'in-memory', firstTimestampBehavior:'cross-track-offset' };
  if(res) opts.audio = { codec:'opus', sampleRate:48000, numberOfChannels:audioCh };
  const muxer = new Muxer(opts);

  let encErr = null;
  const venc = new VideoEncoder({ output:(c, m) => muxer.addVideoChunk(c, m), error:e => { encErr = e; } });
  venc.configure({ codec:'avc1.42001f', width:W, height:H, bitrate:vbps, framerate:30, latencyMode:'realtime' });

  if(res){
    const aenc = new AudioEncoder({ output:(c, m) => muxer.addAudioChunk(c, m), error:e => { encErr = e; } });
    aenc.configure({ codec:'opus', sampleRate:48000, numberOfChannels:audioCh, bitrate:96000 });
    const planars = [];
    for(let c = 0; c < audioCh; c++) planars.push(res.getChannelData(c));
    const block = 960;
    for(let i = 0; i < res.length; i += block){
      const n = Math.min(block, res.length - i);
      const data = new Float32Array(n * audioCh);
      for(let c = 0; c < audioCh; c++) data.set(planars[c].subarray(i, i + n), c * n);
      aenc.encode(new AudioData({
        format:'f32-planar', sampleRate:48000, numberOfFrames:n,
        numberOfChannels:audioCh, timestamp:Math.round(i / 48000 * 1e6), data
      }));
      if((i / block) % 200 === 0) await tick(0);
    }
    await aenc.flush();
  }

  const canvas = document.createElement('canvas');
  canvas.width = W; canvas.height = H;
  const ctx = canvas.getContext('2d');
  const dur = VT.duration || v.duration || 0;
  let idx = 0;

  const draw = () => {
    if(encErr) return;
    ctx.drawImage(v, 0, 0, W, H);
    const frame = new VideoFrame(canvas, { timestamp: Math.round(v.currentTime * 1e6) });
    venc.encode(frame, { keyFrame: idx % 30 === 0 });
    frame.close();
    idx++;
    if(dur) onProgress(Math.min(1, v.currentTime / dur));
    if(!v.ended) v.requestVideoFrameCallback(draw);
  };
  v.requestVideoFrameCallback(draw);

  try {
    await v.play();
    await new Promise((res2, rej2) => {
      const guard = setTimeout(() => rej2(new Error('转码超时')), (dur || 30) * 2000 + 8000);
      v.onended = () => { clearTimeout(guard); res2(); };
    });
    await venc.flush();
    if(encErr) throw encErr;
    muxer.finalize();
    const blob = new Blob([muxer.target.buffer], { type:'video/mp4' });
    if(!blob.size) throw new Error('编码结果为空');
    onProgress(1);
    return blob;
  } finally {
    URL.revokeObjectURL(url);
    v.remove();
  }
}

/* 实时转码：video.captureStream + MediaRecorder */
async function transcodeVideo(file, mime, vbps, onProgress){
  if(typeof MediaRecorder === 'undefined') throw new Error('浏览器不支持 MediaRecorder');
  if(!MediaRecorder.isTypeSupported(mime)) throw new Error('当前浏览器不支持输出该格式');

  const url = URL.createObjectURL(file);
  const v = document.createElement('video');
  v.src = url; v.playsInline = true; v.preload = 'auto';
  v.style.cssText = 'position:fixed;left:-9999px;top:0;width:2px;height:2px;opacity:0;pointer-events:none';
  document.body.appendChild(v);

  await new Promise((res, rej) => {
    v.onloadedmetadata = res;
    v.onerror = () => rej(new Error('无法解码该视频'));
  });

  const ac = new (window.AudioContext || window.webkitAudioContext)();
  let audioTracks = [];
  try {
    const src = ac.createMediaElementSource(v);
    const dest = ac.createMediaStreamDestination();
    src.connect(dest);
    audioTracks = dest.stream.getAudioTracks();
  } catch(e){}

  let vTracks = [];
  if(v.captureStream) vTracks = v.captureStream().getVideoTracks();
  else if(v.mozCaptureStream) vTracks = v.mozCaptureStream().getVideoTracks();
  const tracks = [...vTracks, ...audioTracks];
  if(!tracks.length){ URL.revokeObjectURL(url); v.remove(); ac.close(); throw new Error('无法捕获视频流'); }

  const stream = new MediaStream(tracks);
  const rec = new MediaRecorder(stream, {
    mimeType: mime,
    videoBitsPerSecond: vbps,
    audioBitsPerSecond: 128000
  });
  const chunks = [];
  rec.ondataavailable = e => { if(e.data && e.data.size) chunks.push(e.data); };
  const stopped = new Promise((res, rej) => { rec.onstop = () => res(); rec.onerror = () => rej(new Error('录制失败')); });
  const duration = VT.duration || v.duration || 0;

  v.ontimeupdate = () => { if(duration) onProgress(Math.min(1, v.currentTime / duration)); };

  let cancelled = false;
  const cleanup = () => {
    try { v.pause(); } catch(e){}
    URL.revokeObjectURL(url);
    v.remove();
    try { ac.close(); } catch(e){}
  };

  try {
    rec.start(1000);
    await v.play();
    await new Promise((res, rej) => {
      const guard = setTimeout(() => rej(new Error('转码超时')), (duration || 30) * 2000 + 8000);
      v.onended = () => { clearTimeout(guard); res(); };
    });
    await tick(120);
    if(rec.state !== 'inactive') rec.stop();
    await stopped;
    onProgress(1);
    if(!chunks.length) throw new Error('未捕获到有效数据');
    const out = new Blob(chunks, { type: mime });
    cleanup();
    return out;
  } catch(e){
    try { if(rec.state !== 'inactive') rec.stop(); } catch(_){}
    cleanup();
    throw e;
  }
}

/* WAV 编码 */
function encodeWAV(buf){
  const ch = buf.numberOfChannels, sr = buf.sampleRate, frames = buf.length;
  const bytes = 44 + frames * ch * 2;
  const ab = new ArrayBuffer(bytes);
  const dv = new DataView(ab);
  const wstr = (off, s) => { for(let i = 0; i < s.length; i++) dv.setUint8(off + i, s.charCodeAt(i)); };
  wstr(0, 'RIFF'); dv.setUint32(4, bytes - 8, true); wstr(8, 'WAVE');
  wstr(12, 'fmt '); dv.setUint32(16, 16, true); dv.setUint16(20, 1, true);
  dv.setUint16(22, ch, true); dv.setUint32(24, sr, true);
  dv.setUint32(28, sr * ch * 2, true); dv.setUint16(32, ch * 2, true); dv.setUint16(34, 16, true);
  wstr(36, 'data'); dv.setUint32(40, frames * ch * 2, true);
  const chans = [];
  for(let c = 0; c < ch; c++) chans.push(buf.getChannelData(c));
  let off = 44;
  for(let i = 0; i < frames; i++){
    for(let c = 0; c < ch; c++){
      const s = Math.max(-1, Math.min(1, chans[c][i]));
      dv.setInt16(off, s < 0 ? s * 0x8000 : s * 0x7FFF, true);
      off += 2;
    }
  }
  return new Blob([ab], { type:'audio/wav' });
}

/* MP3 编码（lamejs，按需加载） */
function loadLame(){
  if(window.lamejs) return Promise.resolve(window.lamejs);
  return new Promise((res, rej) => {
    const s = document.createElement('script');
    s.src = 'https://fastly.jsdelivr.net/npm/lamejs@1.2.1/lame.min.js';
    s.onload = () => window.lamejs ? res(window.lamejs) : rej(new Error('MP3 编码器加载失败'));
    s.onerror = () => rej(new Error('MP3 编码器加载失败，请改用 WAV'));
    document.head.appendChild(s);
  });
}
async function encodeMP3(buf, kbps, onProgress){
  const lame = await loadLame();
  const ch = Math.min(2, buf.numberOfChannels);
  const sr = buf.sampleRate;
  const enc = new lame.Mp3Encoder(ch, sr, kbps);
  const to16 = data => { const a = new Int16Array(data.length); for(let i = 0; i < data.length; i++){ const s = Math.max(-1, Math.min(1, data[i])); a[i] = s < 0 ? s * 0x8000 : s * 0x7FFF; } return a; };
  const L = to16(buf.getChannelData(0));
  const R = ch > 1 ? to16(buf.getChannelData(1)) : L;
  const block = 1152, parts = [];
  for(let i = 0; i < L.length; i += block){
    const d = enc.encodeBuffer(L.subarray(i, i + block), R.subarray(i, i + block));
    if(d.length) parts.push(new Int8Array(d));
    if((i / block) % 240 === 0){
      onProgress(i / L.length * .98);
      await tick(0);
    }
  }
  const tail = enc.flush();
  if(tail.length) parts.push(new Int8Array(tail));
  onProgress(1);
  return new Blob(parts, { type:'audio/mpeg' });
}

/* ---------- 事件绑定 ---------- */
function bindEvents(){
  $('importBtn').onclick = e => {
    e.stopPropagation();
    showPop($('importBtn'), [
      { label:'导入文件夹', icon:'i-folder', fn:()=>$('dirInput').click() },
      { label:'选择文件（图片 / 视频 / 音频）', icon:'i-file', fn:()=>$('fileInput').click() },
      { sep:true },
      { label:'重新扫描当前文件夹', icon:'i-search', fn:()=>toast('请在系统文件夹中重新选择同一目录') }
    ]);
  };
  $('fileInput').onchange = e => { importFiles(e.target.files); e.target.value = ''; };
  $('dirInput').onchange = e => { importFiles(e.target.files); e.target.value = ''; };
  $('videoInput').onchange = e => {
    const f = e.target.files && e.target.files[0];
    if(f) setVideoFile(f);
    e.target.value = '';
  };

  $('themeBtn').onclick = () => setTheme(document.documentElement.dataset.theme === 'dark' ? 'light' : 'dark');
  $('sortBtn').onclick = e => {
    e.stopPropagation();
    showPop($('sortBtn'), SORTS.map(s => ({ label:s.label, on:S.sort===s.key, fn:()=>{ S.sort = s.key; renderAll(); } })));
  };
  $('densityBtn').onclick = () => {
    S.density = S.density === 'md' ? 'lg' : S.density === 'lg' ? 'sm' : 'md';
    localStorage.setItem('lumen-density', S.density);
    renderAll();
    toast({sm:'小缩略图',md:'中缩略图',lg:'大缩略图'}[S.density]);
  };
  $('selectBtn').onclick = () => {
    S.selectMode = !S.selectMode;
    if(!S.selectMode) S.selected.clear();
    $('selectBtn').setAttribute('aria-pressed', S.selectMode ? 'true' : 'false');
    renderAll();
  };
  $('searchInput').oninput = e => {
    clearTimeout(window._sh);
    window._sh = setTimeout(() => { S.search = e.target.value.trim(); renderAll(); }, 180);
  };

  // 侧栏导航
  document.querySelector('.nav').addEventListener('click', e => {
    if(e.target.closest('#convertBtn')){ openConvert(); return; }
    if(e.target.closest('#videoBtn')){ openVideoTool(); return; }
    const item = e.target.closest('.nav-item');
    if(!item) return;
    if(item.dataset.album){
      S.view = 'album'; S.albumId = item.dataset.album;
      S.catFilter = null; S.personFilter = null;
    } else if(item.dataset.view){
      const v = item.dataset.view;
      S.view = v; S.catFilter = null; S.personFilter = null; S.albumId = null;
    }
    renderAll();
    if(innerWidth <= 900) $('sidebar').classList.remove('on');
  });
  $('newAlbumBtn').onclick = e => { e.stopPropagation(); newAlbumDialog(); };
  $('menuBtn').onclick = () => $('sidebar').classList.toggle('on');

  // 网格点击
  $('contentInner').addEventListener('click', e => {
    const tile = e.target.closest('.tile');
    if(!tile) return;
    const id = tile.dataset.id;
    if(S.selectMode){
      if(S.selected.has(id)) S.selected.delete(id); else S.selected.add(id);
      renderAll();
    } else openDetail(id);
  });
  $('contentInner').addEventListener('dblclick', e => {
    const tile = e.target.closest('.tile');
    if(!tile || S.selectMode) return;
    openViewer(tile.dataset.id);
  });

  // 详情
  $('dClose').onclick = closeDrawer;
  $('dOpen').onclick = () => { if(S.detailId){ closeDrawer(); openViewer(S.detailId); } };
  $('dRemove').onclick = () => { if(S.detailId) confirmRemove([S.detailId]); };
  $('dExport').onclick = () => {
    const p = S.photos.find(x => x.id === S.detailId);
    if(p) openConvert([p]);
  };

  // 全屏查看
  $('vClose').onclick = closeViewer;
  $('vPrev').onclick = () => stepViewer(-1);
  $('vNext').onclick = () => stepViewer(1);
  $('vImg').onclick = () => $('vImg').classList.toggle('zoom');
  $('vFav').onclick = async () => {
    const p = viewerList[S.viewerIdx]; if(!p) return;
    p.fav = !p.fav; await dbPut('photos', p); syncViewerFav(); renderAll();
  };
  $('vInfo').onclick = () => { const p = viewerList[S.viewerIdx]; if(p){ closeViewer(); openDetail(p.id); } };

  // 批量操作
  $('selClear').onclick = () => { S.selected.clear(); renderAll(); };
  $('selFav').onclick = async () => {
    const ids = [...S.selected];
    for(const id of ids){ const p = S.photos.find(x=>x.id===id); if(p){ p.fav = true; await dbPut('photos', p); } }
    toast(`已收藏 ${ids.length} 张`); renderAll();
  };
  $('selCat').onclick = e => {
    e.stopPropagation();
    showPop($('selCat'), CAT_KEYS.map(k => ({ label:CATS[k].label, fn:async () => {
      const ids = [...S.selected];
      for(const id of ids){ const p = S.photos.find(x=>x.id===id); if(p){ p.cat = k; await dbPut('photos', p); } }
      toast(`已归入「${CATS[k].label}」`); renderAll();
    }})));
  };
  $('selAlbum').onclick = () => pickAlbum([...S.selected]);
  $('selConvert').onclick = () => { if(S.selected.size) openConvert(); };
  $('selRotate').onclick = e => {
    e.stopPropagation();
    showPop($('selRotate'), [
      { label:'左转 90°', icon:'i-rotate', fn:()=>rotateSelected('ccw') },
      { label:'右转 90°', icon:'i-rotate', fn:()=>rotateSelected('cw') },
      { label:'旋转 180°', icon:'i-rotate', fn:()=>rotateSelected('180') },
      { label:'水平翻转', icon:'i-rotate', fn:()=>rotateSelected('flip') }
    ]);
  };
  $('selRemove').onclick = () => confirmRemove([...S.selected]);

  // 模态关闭
  $('modal').addEventListener('click', e => { if(e.target === $('modal')) closeModal(); });
  document.addEventListener('click', e => {
    if(!e.target.closest('#pop') && !e.target.closest('#importBtn') && !e.target.closest('#sortBtn') && !e.target.closest('#selCat') && !e.target.closest('#selRotate')) hidePop();
  });

  // 键盘
  document.addEventListener('keydown', e => {
    if((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 'k'){
      e.preventDefault(); $('searchInput').focus();
    }
    if(e.key === 'Escape'){
      if($('viewer').classList.contains('on')) closeViewer();
      else if($('modal').classList.contains('on')) closeModal();
      else if($('drawer').classList.contains('on')) closeDrawer();
      else hidePop();
    }
    if($('viewer').classList.contains('on')){
      if(e.key === 'ArrowLeft') stepViewer(-1);
      if(e.key === 'ArrowRight') stepViewer(1);
    }
  });

  // 拖拽导入
  const content = $('content');
  let dragDepth = 0;
  window.addEventListener('dragenter', e => { e.preventDefault(); dragDepth++; });
  window.addEventListener('dragover', e => { e.preventDefault(); });
  window.addEventListener('dragleave', e => { e.preventDefault(); dragDepth--; });
  window.addEventListener('drop', async e => {
    e.preventDefault(); dragDepth = 0;
    const fr = $('dropFrame'); if(fr) fr.classList.remove('drag');
    const dt = e.dataTransfer;
    let entries = [];
    try {
      if(dt.items && dt.items.length && dt.items[0].webkitGetAsEntry){
        entries = Array.from(dt.items).map(it => it.webkitGetAsEntry && it.webkitGetAsEntry()).filter(Boolean);
      }
    } catch(err){}
    if(entries.length && entries.some(en => en.isDirectory)){
      toast('正在读取文件夹…');
      const out = [];
      for(const en of entries) await collectEntry(en, out, '');
      importFiles(out);
      return;
    }
    if(dt.files && dt.files.length) importFiles(dt.files);
  });
  content.addEventListener('dragover', e => {
    const fr = $('dropFrame');
    if(fr && e.dataTransfer.types.includes('Files')) fr.classList.add('drag');
  });
  content.addEventListener('dragleave', () => { const fr = $('dropFrame'); if(fr) fr.classList.remove('drag'); });

  window.addEventListener('resize', () => { clearTimeout(window._rz); window._rz = setTimeout(renderGrid, 180); });
}

/* ---------- 启动 ---------- */
function runSplash(){
  const el = $('splash');
  if(!el) return;
  const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  setTimeout(() => {
    el.classList.add('out');
    setTimeout(() => el.remove(), 500);
  }, reduce ? 260 : 1280);
}

function initGlass(){
  const els = Array.from(document.querySelectorAll('.sidebar,.topbar,.drawer,.modal-card,.pop,.toast,.selbar'));
  let raf = 0, lx = 0, ly = 0;
  const paint = () => {
    raf = 0;
    els.forEach(el => {
      const r = el.getBoundingClientRect();
      if(!r.width) return;
      el.style.setProperty('--gx', (lx - r.left) + 'px');
      el.style.setProperty('--gy', (ly - r.top) + 'px');
      el.style.setProperty('--gs', '1');
    });
  };
  addEventListener('pointermove', e => {
    lx = e.clientX; ly = e.clientY;
    if(!raf) raf = requestAnimationFrame(paint);
  }, { passive:true });
  document.addEventListener('pointerleave', () => {
    els.forEach(el => el.style.setProperty('--gs', '0'));
  });
}

async function boot(){
  fillAppMeta();
  initGlass();
  runSplash();
  const savedTheme = localStorage.getItem('lumen-theme');
  setTheme(savedTheme || (matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark'));
  S.density = localStorage.getItem('lumen-density') || 'md';
  S.sort = localStorage.getItem('lumen-sort') || 'added_desc';

  try {
    await openDB();
    S.photos = await dbAll('photos');
    S.albums = await dbAll('albums');
  } catch(e){
    toast('本地存储不可用，请用 Chrome / Edge 打开');
  }
  bindEvents();
  renderAll();
  if(innerWidth <= 900) $('menuBtn').style.display = 'grid';
}
boot();

</script>
</body>
</html>
