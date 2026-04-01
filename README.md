#TRUYỆN
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Góc Truyện Của Tôi</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
<style>
:root {
  --bg:#FAF8F4; --bg-card:#FFFFFF; --text-main:#1C1917; --text-muted:#78716C;
  --text-hint:#A8A29E; --accent:#92400E; --accent-light:#FEF3C7; --accent-mid:#D97706;
  --border:#E7E5E4; --border-strong:#D6D3D1; --tag-bg:#F5F0E8; --tag-text:#78400E;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text-main);line-height:1.7;min-height:100vh;}
header{background:var(--bg-card);border-bottom:1px solid var(--border);padding:0 2rem;position:sticky;top:0;z-index:100;display:flex;align-items:center;justify-content:space-between;height:64px;}
.logo{font-family:'Playfair Display',serif;font-size:1.4rem;color:var(--accent);cursor:pointer;}
nav{display:flex;gap:2rem;}
nav a{text-decoration:none;color:var(--text-muted);font-size:0.9rem;font-weight:500;cursor:pointer;transition:color 0.2s;}
nav a:hover,nav a.active{color:var(--text-main);}
.page{display:none;} .page.active{display:block;}

/* HOME */
.hero{max-width:860px;margin:4rem auto 2.5rem;padding:0 2rem;text-align:center;}
.hero h1{font-family:'Playfair Display',serif;font-size:clamp(2rem,5vw,3.2rem);line-height:1.15;margin-bottom:0.8rem;}
.hero h1 em{font-style:italic;color:var(--accent-mid);}
.hero p{color:var(--text-muted);font-size:1rem;max-width:460px;margin:0 auto;}
.controls{max-width:900px;margin:0 auto 1.5rem;padding:0 2rem;display:flex;flex-direction:column;gap:0.9rem;}
.search-box{position:relative;}
.search-box input{width:100%;padding:0.65rem 1rem 0.65rem 2.6rem;border:1px solid var(--border-strong);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.9rem;background:var(--bg-card);color:var(--text-main);outline:none;transition:border-color 0.2s;}
.search-box input:focus{border-color:var(--accent-mid);}
.search-icon{position:absolute;left:0.85rem;top:50%;transform:translateY(-50%);color:var(--text-hint);font-size:0.85rem;pointer-events:none;}
.filter-row{display:flex;gap:0.5rem;flex-wrap:wrap;align-items:center;}
.filter-label{font-size:0.72rem;color:var(--text-hint);font-weight:500;text-transform:uppercase;letter-spacing:0.05em;margin-right:0.15rem;}
.filter-btn{padding:0.38rem 0.9rem;border:1px solid var(--border-strong);border-radius:99px;background:var(--bg-card);color:var(--text-muted);font-family:'DM Sans',sans-serif;font-size:0.8rem;font-weight:500;cursor:pointer;transition:all 0.2s;white-space:nowrap;}
.filter-btn:hover{border-color:var(--accent-mid);color:var(--accent);}
.filter-btn.active{background:var(--accent);border-color:var(--accent);color:#FFF;}
.divider-v{width:1px;height:18px;background:var(--border-strong);margin:0 0.2rem;}

.story-grid{max-width:900px;margin:0 auto;padding:0 2rem 5rem;display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:1.5rem;}
.story-card{background:var(--bg-card);border:1px solid var(--border);border-radius:12px;overflow:hidden;transition:transform 0.2s,box-shadow 0.2s;cursor:pointer;display:flex;flex-direction:column;}
.story-card:hover{transform:translateY(-3px);box-shadow:0 12px 32px rgba(0,0,0,0.08);}
.story-card-cover{height:128px;display:flex;align-items:center;justify-content:center;font-family:'Playfair Display',serif;font-size:2.2rem;font-style:italic;color:rgba(255,255,255,0.9);}
.story-card-body{padding:1rem 1.2rem 1.2rem;flex:1;display:flex;flex-direction:column;}
.tag-row{display:flex;gap:0.4rem;flex-wrap:wrap;margin-bottom:0.55rem;}
.tag{display:inline-block;font-size:0.69rem;font-weight:500;padding:2px 9px;border-radius:99px;text-transform:uppercase;letter-spacing:0.04em;}
.tag-genre{background:#EDE9FE;color:#5B21B6;}
.tag-type{background:var(--tag-bg);color:var(--tag-text);}
.story-title{font-family:'Playfair Display',serif;font-size:1.05rem;font-weight:600;line-height:1.3;margin-bottom:0.35rem;}
.story-desc{font-size:0.82rem;color:var(--text-muted);line-height:1.6;flex:1;display:-webkit-box;-webkit-line-clamp:3;-webkit-box-orient:vertical;overflow:hidden;}
.story-meta{display:flex;align-items:center;justify-content:space-between;margin-top:0.9rem;padding-top:0.7rem;border-top:1px solid var(--border);font-size:0.77rem;color:var(--text-hint);}
.read-btn{color:var(--accent-mid);font-weight:500;}
.empty-state{grid-column:1/-1;text-align:center;padding:4rem 0;color:var(--text-hint);}
.empty-state p{margin-top:0.5rem;font-size:0.9rem;}

/* STORY DETAIL */
.story-header{max-width:720px;margin:3rem auto 1.5rem;padding:0 2rem;}
.back-btn{display:inline-flex;align-items:center;gap:0.4rem;color:var(--text-muted);font-size:0.85rem;cursor:pointer;margin-bottom:1.2rem;transition:color 0.2s;border:none;background:none;font-family:'DM Sans',sans-serif;padding:0;}
.back-btn:hover{color:var(--text-main);}
.cover-banner{height:108px;border-radius:12px;margin-bottom:1.2rem;display:flex;align-items:center;padding:0 2rem;font-family:'Playfair Display',serif;font-size:2.3rem;font-style:italic;color:rgba(255,255,255,0.9);}
.chapter-list{max-width:720px;margin:0 auto;padding:0 2rem 5rem;}
.chapter-list h3{font-size:0.72rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--text-hint);font-weight:500;margin-bottom:0.6rem;}
.chapter-item{display:flex;align-items:center;padding:0.78rem 1rem;border:1px solid var(--border);border-radius:8px;margin-bottom:0.4rem;background:var(--bg-card);cursor:pointer;transition:all 0.2s;}
.chapter-item:hover{border-color:var(--accent-mid);background:var(--accent-light);}
.chapter-num{font-size:0.72rem;color:var(--text-hint);font-weight:500;min-width:72px;}
.chapter-name{flex:1;font-size:0.9rem;}
.chapter-arrow{color:var(--text-hint);}

/* READING */
.reading-header{max-width:660px;margin:3rem auto 1.5rem;padding:0 2rem;}
.reading-nav{display:flex;align-items:center;gap:0.5rem;margin-bottom:1.75rem;font-size:0.82rem;color:var(--text-muted);flex-wrap:wrap;}
.reading-nav span{cursor:pointer;} .reading-nav span:hover{color:var(--text-main);}
.reading-nav .sep{color:var(--border-strong);cursor:default;}
.reading-nav .current{color:var(--text-main);cursor:default;}
.reading-title{font-family:'Playfair Display',serif;font-size:clamp(1.5rem,3.5vw,2rem);margin-bottom:0.3rem;line-height:1.25;}
.reading-info{color:var(--text-hint);font-size:0.82rem;margin-bottom:2.5rem;}
.reading-body{max-width:660px;margin:0 auto;padding:0 2rem 4rem;font-size:1.05rem;line-height:1.95;color:#2C2A28;}
.reading-body p{margin-bottom:1.4em;}
.reading-body h2{font-family:'Playfair Display',serif;font-size:1.2rem;margin:2em 0 0.75em;}
.chapter-footer{max-width:660px;margin:0 auto 5rem;padding:0 2rem;display:flex;justify-content:space-between;gap:1rem;}
.nav-btn{padding:0.6rem 1.4rem;border:1px solid var(--border-strong);border-radius:8px;background:var(--bg-card);font-family:'DM Sans',sans-serif;font-size:0.85rem;color:var(--text-muted);cursor:pointer;transition:all 0.2s;font-weight:500;}
.nav-btn:hover:not(:disabled){border-color:var(--accent-mid);color:var(--accent);}
.nav-btn:disabled{opacity:0.3;cursor:not-allowed;}

/* ABOUT */
.about-wrap{max-width:660px;margin:5rem auto;padding:0 2rem 5rem;}
.about-wrap h1{font-family:'Playfair Display',serif;font-size:2rem;margin-bottom:1.5rem;}
.about-wrap p{color:var(--text-muted);margin-bottom:1.1rem;font-size:0.97rem;line-height:1.8;}

/* ADMIN */
.admin-wrap{max-width:720px;margin:3rem auto;padding:0 2rem 5rem;}
.admin-wrap h1{font-family:'Playfair Display',serif;font-size:1.8rem;margin-bottom:0.4rem;}
.admin-subtitle{color:var(--text-muted);font-size:0.88rem;margin-bottom:2rem;}
.admin-section{background:var(--bg-card);border:1px solid var(--border);border-radius:12px;padding:1.5rem;margin-bottom:1.25rem;}
.admin-section h2{font-size:0.95rem;font-weight:500;margin-bottom:1.2rem;color:var(--text-main);}
.form-row{margin-bottom:1rem;}
.form-row label{display:block;font-size:0.75rem;font-weight:500;color:var(--text-muted);margin-bottom:0.3rem;text-transform:uppercase;letter-spacing:0.04em;}
.form-row input,.form-row select,.form-row textarea{width:100%;padding:0.58rem 0.85rem;border:1px solid var(--border-strong);border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.9rem;color:var(--text-main);background:var(--bg);outline:none;transition:border-color 0.2s;}
.form-row input:focus,.form-row select:focus,.form-row textarea:focus{border-color:var(--accent-mid);}
.form-row textarea{min-height:78px;resize:vertical;}
.form-row-2{display:grid;grid-template-columns:1fr 1fr;gap:0.75rem;}
.upload-zone{border:2px dashed var(--border-strong);border-radius:10px;padding:1.75rem;text-align:center;cursor:pointer;transition:all 0.2s;background:var(--bg);}
.upload-zone:hover,.upload-zone.drag-over{border-color:var(--accent-mid);background:var(--accent-light);}
.upload-zone .icon{font-size:1.75rem;}
.upload-zone strong{font-size:0.88rem;}
.upload-zone p{color:var(--text-muted);font-size:0.82rem;margin-top:0.3rem;}
#word-file-input{display:none;}
.chapter-preview{border:1px solid var(--border);border-radius:8px;padding:0.75rem 1rem;margin-top:0.6rem;background:var(--bg);display:flex;align-items:center;justify-content:space-between;}
.chapter-preview span{font-size:0.85rem;}
.chapter-preview button{background:none;border:none;color:var(--text-hint);cursor:pointer;font-size:1rem;padding:0;transition:color 0.2s;}
.chapter-preview button:hover{color:#DC2626;}
.btn-primary{background:var(--accent);color:#FFF;border:none;padding:0.62rem 1.4rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.88rem;font-weight:500;cursor:pointer;transition:background 0.2s;}
.btn-primary:hover{background:#78350F;}
.btn-secondary{background:var(--bg-card);color:var(--text-main);border:1px solid var(--border-strong);padding:0.58rem 1.1rem;border-radius:8px;font-family:'DM Sans',sans-serif;font-size:0.88rem;cursor:pointer;transition:all 0.2s;}
.btn-secondary:hover{border-color:var(--accent-mid);}
.story-manage-item{display:flex;align-items:center;justify-content:space-between;padding:0.72rem 1rem;border:1px solid var(--border);border-radius:8px;margin-bottom:0.4rem;background:var(--bg);}
.story-manage-name{font-size:0.88rem;font-weight:500;}
.story-manage-meta{font-size:0.73rem;color:var(--text-hint);margin-top:2px;}
.btn-sm{padding:0.3rem 0.75rem;font-size:0.76rem;border-radius:6px;border:1px solid var(--border-strong);background:var(--bg-card);color:var(--text-muted);cursor:pointer;font-family:'DM Sans',sans-serif;transition:all 0.2s;}
.btn-sm.danger:hover{border-color:#DC2626;color:#DC2626;}
.color-picker-row{display:flex;gap:0.45rem;flex-wrap:wrap;}
.color-opt{width:30px;height:30px;border-radius:6px;cursor:pointer;border:2px solid transparent;transition:border-color 0.15s;}
.color-opt.selected{border-color:var(--text-main);}
.toast{position:fixed;bottom:2rem;right:2rem;background:#1C1917;color:#FFF;padding:0.7rem 1.2rem;border-radius:8px;font-size:0.83rem;z-index:999;opacity:0;transition:opacity 0.3s;pointer-events:none;}
.toast.show{opacity:1;}
@media(max-width:600px){header{padding:0 1rem;}nav{gap:1.2rem;}.story-grid{grid-template-columns:1fr;}.form-row-2{grid-template-columns:1fr;}}
</style>
</head>
<body>

<header>
  <div class="logo" onclick="goHome()">✦ Góc Truyện</div>
  <nav>
    <a onclick="goHome()" id="nav-home" class="active">Trang chủ</a>
    <a onclick="goAbout()" id="nav-about">Tác giả</a>
    <a onclick="goAdmin()" id="nav-admin">Quản lý</a>
  </nav>
</header>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="hero">
    <h1>Những câu chuyện<br><em>từ trái tim tôi</em></h1>
    <p>Tập hợp các truyện ngắn và dài kỳ do mình tự viết. Mỗi câu chuyện là một chuyến đi nhỏ.</p>
  </div>
  <div class="controls">
    <div class="search-box">
      <span class="search-icon">🔍</span>
      <input type="text" id="search-input" placeholder="Tìm tên truyện..." oninput="applyFilters()">
    </div>
    <div class="filter-row">
      <span class="filter-label">Thể loại</span>
      <button class="filter-btn active" data-fkey="genre" data-fval="all" onclick="setFilter('genre','all',this)">Tất cả</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Tu Tiên" onclick="setFilter('genre','Tu Tiên',this)">Tu Tiên</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Boy Love" onclick="setFilter('genre','Boy Love',this)">Boy Love</button>
      <button class="filter-btn" data-fkey="genre" data-fval="Xuyên Không/Trùng Sinh" onclick="setFilter('genre','Xuyên Không/Trùng Sinh',this)">Xuyên Không / Trùng Sinh</button>
      <div class="divider-v"></div>
      <span class="filter-label">Dạng</span>
      <button class="filter-btn active" data-fkey="type" data-fval="all" onclick="setFilter('type','all',this)">Tất cả</button>
      <button class="filter-btn" data-fkey="type" data-fval="Oneshot" onclick="setFilter('type','Oneshot',this)">Oneshot</button>
      <button class="filter-btn" data-fkey="type" data-fval="Truyện Dài" onclick="setFilter('type','Truyện Dài',this)">Truyện Dài</button>
    </div>
  </div>
  <div class="story-grid" id="story-grid"></div>
</div>

<!-- STORY DETAIL -->
<div class="page" id="page-story">
  <div class="story-header">
    <button class="back-btn" onclick="goHome()">← Quay lại</button>
    <div class="cover-banner" id="detail-banner"></div>
    <h1 id="detail-title" style="font-family:'Playfair Display',serif;font-size:clamp(1.6rem,4vw,2.3rem);margin-bottom:0.4rem;"></h1>
    <div id="detail-tags" style="display:flex;gap:0.4rem;margin-bottom:0.8rem;"></div>
    <p id="detail-desc" style="color:var(--text-muted);font-size:0.92rem;"></p>
  </div>
  <div class="chapter-list">
    <h3>Danh sách chương</h3>
    <div id="chapter-items"></div>
  </div>
</div>

<!-- READING -->
<div class="page" id="page-reading">
  <div class="reading-header">
    <div class="reading-nav">
      <span onclick="goHome()">Trang chủ</span>
      <span class="sep">›</span>
      <span id="nav-story-name" onclick="goBackToStory()"></span>
      <span class="sep">›</span>
      <span class="current" id="nav-chapter-name"></span>
    </div>
    <div class="reading-title" id="read-title"></div>
    <div class="reading-info" id="read-info"></div>
  </div>
  <div class="reading-body" id="read-body"></div>
  <div class="chapter-footer">
    <button class="nav-btn" id="btn-prev" onclick="navChapter(-1)">← Chương trước</button>
    <button class="nav-btn" id="btn-next" onclick="navChapter(1)">Chương tiếp →</button>
  </div>
</div>

<!-- ABOUT -->
<div class="page" id="page-about">
  <div class="about-wrap">
    <h1>Về tác giả</h1>
    <p>Xin chào! Mình là [Tên của bạn], một người yêu thích viết lách và kể chuyện.</p>
    <p>Trang web này là nơi mình lưu giữ và chia sẻ những câu chuyện mình tự viết — từ những mẩu oneshot viết trong đêm khuya đến những bộ truyện dài hơi ấp ủ từ lâu.</p>
    <p>Cảm ơn bạn đã ghé thăm và đọc truyện của mình!</p>
  </div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <div class="admin-wrap">
    <h1>Quản lý truyện</h1>
    <p class="admin-subtitle">Thêm truyện mới, upload chương từ file Word, rồi xuất file HTML để đưa lên web.</p>

    <div class="admin-section">
      <h2>➕ Thêm truyện mới</h2>
      <div class="form-row"><label>Tên truyện</label><input type="text" id="new-title" placeholder="VD: Tiên Đạo Vô Danh"></div>
      <div class="form-row"><label>Mô tả ngắn</label><textarea id="new-desc" placeholder="Viết vài dòng giới thiệu..."></textarea></div>
      <div class="form-row-2">
        <div class="form-row" style="margin:0"><label>Thể loại</label>
          <select id="new-genre">
            <option value="Tu Tiên">Tu Tiên</option>
            <option value="Boy Love">Boy Love</option>
            <option value="Xuyên Không/Trùng Sinh">Xuyên Không / Trùng Sinh</option>
          </select>
        </div>
        <div class="form-row" style="margin:0"><label>Dạng truyện</label>
          <select id="new-type">
            <option value="Oneshot">Oneshot</option>
            <option value="Truyện Dài">Truyện Dài</option>
          </select>
        </div>
      </div>
      <div class="form-row"><label>Màu bìa</label>
        <div class="color-picker-row" id="color-picker">
          <div class="color-opt selected" data-color="linear-gradient(135deg,#F59E0B,#D97706)" style="background:linear-gradient(135deg,#F59E0B,#D97706)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#6366F1,#4338CA)" style="background:linear-gradient(135deg,#6366F1,#4338CA)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#10B981,#059669)" style="background:linear-gradient(135deg,#10B981,#059669)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#EC4899,#BE185D)" style="background:linear-gradient(135deg,#EC4899,#BE185D)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#EF4444,#DC2626)" style="background:linear-gradient(135deg,#EF4444,#DC2626)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#14B8A6,#0F766E)" style="background:linear-gradient(135deg,#14B8A6,#0F766E)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#8B5CF6,#6D28D9)" style="background:linear-gradient(135deg,#8B5CF6,#6D28D9)"></div>
          <div class="color-opt" data-color="linear-gradient(135deg,#F97316,#EA580C)" style="background:linear-gradient(135deg,#F97316,#EA580C)"></div>
        </div>
      </div>
      <div class="form-row"><label>Chữ hiển thị trên bìa</label><input type="text" id="new-emoji" maxlength="2" placeholder="VD: T" style="max-width:72px;"></div>
      <button class="btn-primary" onclick="addStory()">Tạo truyện</button>
    </div>

    <div class="admin-section">
      <h2>📖 Thêm chương từ file Word</h2>
      <div class="form-row"><label>Chọn truyện</label><select id="chapter-story-select"><option value="">-- Chọn truyện --</option></select></div>
      <div class="form-row"><label>Tên chương</label><input type="text" id="new-chapter-title" placeholder="VD: Chương 1 – Khởi đầu"></div>
      <div class="form-row">
        <label>Upload file Word (.docx)</label>
        <div class="upload-zone" id="upload-zone" onclick="document.getElementById('word-file-input').click()">
          <div class="icon">📄</div>
          <strong>Bấm để chọn file .docx</strong>
          <p>hoặc kéo thả file vào đây</p>
        </div>
        <input type="file" id="word-file-input" accept=".docx" onchange="handleWordFile(this.files[0])">
        <div id="file-preview"></div>
      </div>
      <button class="btn-primary" onclick="addChapter()">Thêm chương</button>
    </div>

    <div class="admin-section">
      <h2>📚 Truyện hiện có</h2>
      <div id="story-manage-list"></div>
    </div>

    <div class="admin-section">
      <h2>💾 Xuất file để đưa lên web</h2>
      <p style="font-size:0.84rem;color:var(--text-muted);margin-bottom:1rem;">Sau khi thêm/sửa xong, bấm xuất để tải file HTML mới về máy. Dữ liệu truyện được nhúng vào bên trong file đó.</p>
      <div style="display:flex;gap:0.75rem;flex-wrap:wrap;">
        <button class="btn-primary" onclick="exportHTML()">⬇ Xuất file HTML</button>
        <button class="btn-secondary" onclick="goHome()">← Xem trang chủ</button>
      </div>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ==== DỮ LIỆU ====
let STORIES = [
  {id:1,title:"Mùa Hè Không Tên",genre:"Xuyên Không/Trùng Sinh",type:"Oneshot",desc:"Câu chuyện về hai người trẻ gặp nhau trong một mùa hè ngắn ngủi, và những kỷ niệm họ để lại cho nhau mãi mãi không phai.",cover:{bg:"linear-gradient(135deg,#F59E0B,#D97706)",emoji:"M"},chapters:[{title:"Buổi chiều đầu tiên",content:"<p>Hà gặp Minh vào một buổi chiều tháng Sáu, khi cơn mưa đầu mùa còn chưa kịp tan.</p><p>Quán cà phê nhỏ hôm ấy đông hơn thường lệ. Hà chọn chiếc ghế cạnh cửa sổ — để những hạt nước li ti bắn vào tay mà không cảm thấy khó chịu, chỉ thấy gì đó dịu nhẹ đến kỳ lạ.</p><p>\"Xin lỗi, chỗ này còn trống không?\"</p><p>Cô ngẩng lên. Một anh chàng đứng trước mặt, tóc ướt một nửa, nụ cười hơi ngại ngùng. Tay cầm chiếc máy ảnh phim cũ, trông như vừa từ năm 1998 bước ra.</p><p>Hà nhìn xung quanh — quán đã kín hết chỗ từ bao giờ.</p><p>\"Được,\" cô nói, rồi dịch chiếc túi vải sang một bên.</p>"}]},
  {id:2,title:"Thiên Đạo Ngược Chiều",genre:"Tu Tiên",type:"Truyện Dài",desc:"Lâm Phong — một tu sĩ phế vật — vô tình nhận được ký ức của tiền bối mạnh nhất thế giới tu tiên. Con đường nghịch thiên bắt đầu từ đây.",cover:{bg:"linear-gradient(135deg,#6366F1,#4338CA)",emoji:"T"},chapters:[{title:"Phế vật thức tỉnh",content:"<p>Không ai ngờ Lâm Phong sẽ sống qua đêm đó.</p><p>Hắn nằm giữa vũng máu, thân thể kinh mạch tấc tấc đứt gãy, căn cơ phá hủy toàn bộ. Trong mắt mọi người của Linh Vân Tông, đây là cái chết đã định.</p><p>Nhưng khi hắn mở mắt ra, thứ đầu tiên hắn thấy là một biển ký ức không thuộc về mình.</p>"},{title:"Con đường nghịch thiên",content:"<p>Ba ngày sau, Lâm Phong rời phòng dưỡng thương.</p><p>Không ai chú ý. Một phế vật sống hay chết có gì quan trọng.</p><p>Nhưng trong đầu hắn lúc này là toàn bộ ký ức của Thiên Đạo Tôn — người từng đứng trên đỉnh cõi tu tiên hàng nghìn năm trước, người duy nhất phá vỡ giới hạn Hóa Thần.</p>"}]},
  {id:3,title:"Mưa Rơi Ở Thành Phố Người",genre:"Boy Love",type:"Truyện Dài",desc:"Kiên và Hữu — hai người đàn ông, hai tính cách trái ngược — tình cờ trở thành hàng xóm. Mưa Sài Gòn làm chứng cho một tình yêu chậm và lặng lẽ.",cover:{bg:"linear-gradient(135deg,#EC4899,#BE185D)",emoji:"M"},chapters:[{title:"Tầng ba, căn 301",content:"<p>Kiên dọn đến căn 301 vào một sáng thứ Tư, khi trời Sài Gòn đang chuẩn bị đổ mưa.</p><p>Hắn chỉ có một va li và hai thùng sách. Thang máy hỏng. Ba tầng cầu thang hắn đi bảy chuyến.</p><p>Đến chuyến thứ tư, có người ra mở cửa căn 302 và nhìn hắn không nói gì.</p><p>\"Xin chào,\" Kiên nói.</p><p>Người đó — tóc rối, mặc áo thun cũ — gật đầu rồi đóng cửa lại.</p>"}]}
];

let activeFilters = {genre:'all', type:'all'};
let currentStoryId = null, currentChapterIdx = null;
let pendingContent = null;
let selectedColor = "linear-gradient(135deg,#F59E0B,#D97706)";

// ==== FILTER ====
function setFilter(key, val, btn) {
  activeFilters[key] = val;
  document.querySelectorAll(`[data-fkey="${key}"]`).forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  applyFilters();
}

function applyFilters() {
  const q = (document.getElementById('search-input').value || '').toLowerCase();
  const result = STORIES.filter(s => {
    const okGenre = activeFilters.genre === 'all' || s.genre === activeFilters.genre;
    const okType  = activeFilters.type  === 'all' || s.type  === activeFilters.type;
    const okQuery = !q || s.title.toLowerCase().includes(q) || s.desc.toLowerCase().includes(q);
    return okGenre && okType && okQuery;
  });
  renderStories(result);
}

function renderStories(list) {
  const grid = document.getElementById('story-grid');
  grid.innerHTML = '';
  if (!list.length) {
    grid.innerHTML = '<div class="empty-state"><div style="font-size:2rem">📖</div><p>Không tìm thấy truyện nào phù hợp.</p></div>';
    return;
  }
  list.forEach(s => {
    const el = document.createElement('div');
    el.className = 'story-card';
    el.onclick = () => openStory(s.id);
    el.innerHTML = `<div class="story-card-cover" style="background:${s.cover.bg}">${s.cover.emoji}</div>
      <div class="story-card-body">
        <div class="tag-row"><span class="tag tag-genre">${s.genre}</span><span class="tag tag-type">${s.type}</span></div>
        <div class="story-title">${s.title}</div>
        <div class="story-desc">${s.desc}</div>
        <div class="story-meta"><span>${s.chapters.length} chương</span><span class="read-btn">Đọc ngay →</span></div>
      </div>`;
    grid.appendChild(el);
  });
}

// ==== STORY DETAIL ====
function openStory(id) {
  const s = STORIES.find(x => x.id === id);
  if (!s) return;
  currentStoryId = id;
  document.getElementById('detail-banner').style.background = s.cover.bg;
  document.getElementById('detail-banner').textContent = s.cover.emoji;
  document.getElementById('detail-title').textContent = s.title;
  document.getElementById('detail-desc').textContent = s.desc;
  document.getElementById('detail-tags').innerHTML = `<span class="tag tag-genre">${s.genre}</span><span class="tag tag-type">${s.type}</span>`;
  const items = document.getElementById('chapter-items');
  items.innerHTML = '';
  s.chapters.forEach((ch, i) => {
    const el = document.createElement('div');
    el.className = 'chapter-item';
    el.onclick = () => openChapter(id, i);
    el.innerHTML = `<span class="chapter-num">Chương ${i+1}</span><span class="chapter-name">${ch.title}</span><span class="chapter-arrow">›</span>`;
    items.appendChild(el);
  });
  showPage('page-story');
}

function openChapter(sid, idx) {
  const s = STORIES.find(x => x.id === sid);
  if (!s) return;
  currentStoryId = sid; currentChapterIdx = idx;
  const ch = s.chapters[idx];
  document.getElementById('nav-story-name').textContent = s.title;
  document.getElementById('nav-chapter-name').textContent = `Chương ${idx+1}`;
  document.getElementById('read-title').textContent = ch.title;
  document.getElementById('read-info').textContent = `${s.title} • Chương ${idx+1} / ${s.chapters.length}`;
  document.getElementById('read-body').innerHTML = ch.content;
  document.getElementById('btn-prev').disabled = idx === 0;
  document.getElementById('btn-next').disabled = idx === s.chapters.length-1;
  showPage('page-reading'); window.scrollTo(0,0);
}

function navChapter(d) {
  const s = STORIES.find(x => x.id === currentStoryId);
  if (!s) return;
  const ni = currentChapterIdx + d;
  if (ni >= 0 && ni < s.chapters.length) openChapter(currentStoryId, ni);
}

function goBackToStory() { openStory(currentStoryId); }

// ==== ADMIN ====
function refreshStorySelect() {
  const sel = document.getElementById('chapter-story-select');
  sel.innerHTML = '<option value="">-- Chọn truyện --</option>';
  STORIES.forEach(s => { const o = document.createElement('option'); o.value=s.id; o.textContent=s.title; sel.appendChild(o); });
}

function refreshManageList() {
  const el = document.getElementById('story-manage-list');
  if (!STORIES.length) { el.innerHTML='<p style="color:var(--text-hint);font-size:0.85rem;">Chưa có truyện nào.</p>'; return; }
  el.innerHTML = STORIES.map(s=>`
    <div class="story-manage-item">
      <div><div class="story-manage-name">${s.title}</div><div class="story-manage-meta">${s.genre} • ${s.type} • ${s.chapters.length} chương</div></div>
      <div><button class="btn-sm danger" onclick="deleteStory(${s.id})">Xóa</button></div>
    </div>`).join('');
}

document.querySelectorAll('.color-opt').forEach(el => {
  el.onclick = () => { document.querySelectorAll('.color-opt').forEach(e=>e.classList.remove('selected')); el.classList.add('selected'); selectedColor=el.dataset.color; };
});

function addStory() {
  const title = document.getElementById('new-title').value.trim();
  const desc  = document.getElementById('new-desc').value.trim();
  const genre = document.getElementById('new-genre').value;
  const type  = document.getElementById('new-type').value;
  const emoji = document.getElementById('new-emoji').value.trim() || (title[0]||'✦');
  if (!title) { showToast('Vui lòng nhập tên truyện!'); return; }
  const newId = STORIES.length ? Math.max(...STORIES.map(s=>s.id))+1 : 1;
  STORIES.push({id:newId, title, genre, type, desc, cover:{bg:selectedColor, emoji}, chapters:[]});
  document.getElementById('new-title').value='';
  document.getElementById('new-desc').value='';
  document.getElementById('new-emoji').value='';
  refreshStorySelect(); refreshManageList();
  showToast('✅ Đã thêm truyện "' + title + '"');
}

function deleteStory(id) {
  if (!confirm('Xóa truyện này?')) return;
  STORIES = STORIES.filter(s=>s.id!==id);
  refreshStorySelect(); refreshManageList(); applyFilters();
  showToast('Đã xóa.');
}

// Word upload
const uploadZone = document.getElementById('upload-zone');
uploadZone.addEventListener('dragover', e=>{e.preventDefault();uploadZone.classList.add('drag-over');});
uploadZone.addEventListener('dragleave', ()=>uploadZone.classList.remove('drag-over'));
uploadZone.addEventListener('drop', e=>{
  e.preventDefault(); uploadZone.classList.remove('drag-over');
  const f=e.dataTransfer.files[0];
  if(f&&f.name.endsWith('.docx')) handleWordFile(f); else showToast('Chỉ hỗ trợ file .docx');
});

function handleWordFile(file) {
  if (!file) return;
  const reader = new FileReader();
  reader.onload = e => {
    mammoth.convertToHtml({arrayBuffer: e.target.result})
      .then(r => {
        pendingContent = r.value;
        document.getElementById('file-preview').innerHTML = `
          <div class="chapter-preview">
            <span>📄 ${file.name} — đã đọc xong</span>
            <button onclick="clearWord()">✕</button>
          </div>`;
        showToast('✅ Đọc file Word thành công!');
      }).catch(()=>showToast('Lỗi đọc file. Thử lại nhé.'));
  };
  reader.readAsArrayBuffer(file);
}

function clearWord() {
  pendingContent=null;
  document.getElementById('file-preview').innerHTML='';
  document.getElementById('word-file-input').value='';
}

function addChapter() {
  const sid   = parseInt(document.getElementById('chapter-story-select').value);
  const title = document.getElementById('new-chapter-title').value.trim();
  if (!sid)           { showToast('Chọn truyện trước!'); return; }
  if (!title)         { showToast('Nhập tên chương!'); return; }
  if (!pendingContent){ showToast('Upload file Word trước!'); return; }
  const story = STORIES.find(s=>s.id===sid);
  story.chapters.push({title, content: pendingContent});
  document.getElementById('new-chapter-title').value='';
  clearWord(); refreshManageList();
  showToast(`✅ Đã thêm "${title}" vào "${story.title}"`);
}

// Export
function exportHTML() {
  const json = JSON.stringify(STORIES, null, 2);
  const src = document.documentElement.outerHTML;
  // Replace the STORIES data block in the exported HTML
  const updated = src.replace(/let STORIES = \[[\s\S]*?\];/, 'let STORIES = ' + json + ';');
  const blob = new Blob([updated], {type:'text/html'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'index.html';
  a.click();
  showToast('✅ Đã tải file HTML mới!');
}

// Toast
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 3000);
}

// Navigation
function showPage(id) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0,0);
  document.querySelectorAll('nav a').forEach(a=>a.classList.remove('active'));
  const map = {'page-home':'nav-home','page-about':'nav-about','page-admin':'nav-admin'};
  if(map[id]) document.getElementById(map[id]).classList.add('active');
}

function goHome()  { showPage('page-home');  applyFilters(); }
function goAbout() { showPage('page-about'); }
function goAdmin() { showPage('page-admin'); refreshStorySelect(); refreshManageList(); }

// Init
applyFilters();
</script>
</body>
</html>
