<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quản lý Tài sản CNTT</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1>HỆ THỐNG QUẢN LÝ TÀI SẢN CNTT</h1>
            <div class="user-info">
                <span id="username-display">Chưa đăng nhập</span>
                <button id="logout-btn" class="btn btn-logout">Đăng xuất</button>
            </div>
        </header>

        <!-- Login Form -->
        <div id="login-section" class="login-container">
            <h2>Đăng nhập hệ thống</h2>
            <form id="login-form">
                <div class="form-group">
                    <label for="username">Tên đăng nhập:</label>
                    <input type="text" id="username" required>
                </div>
                <div class="form-group">
                    <label for="password">Mật khẩu:</label>
                    <input type="password" id="password" required>
                </div>
                <button type="submit" class="btn btn-login">Đăng nhập</button>
            </form>
        </div>

        <!-- Main App (hidden until login) -->
        <div id="app-section" class="app-container" style="display: none;">
            <!-- Navigation -->
            <nav class="sidebar">
                <ul>
                    <li><a href="#" class="nav-link active" data-section="dashboard"><i class="fas fa-tachometer-alt"></i> Dashboard</a></li>
                    <li><a href="#" class="nav-link" data-section="assets"><i class="fas fa-laptop"></i> Quản lý Tài sản</a></li>
                    <li><a href="#" class="nav-link" data-section="documents"><i class="fas fa-file-alt"></i> Văn bản lưu trữ</a></li>
                    <li id="admin-menu" style="display: none;"><a href="#" class="nav-link" data-section="users"><i class="fas fa-users-cog"></i> Quản lý Người dùng</a></li>
                    <li id="report-menu"><a href="#" class="nav-link" data-section="reports"><i class="fas fa-chart-bar"></i> Báo cáo</a></li>
                </ul>
            </nav>

            <!-- Main Content -->
            <main class="main-content">
                <!-- Dashboard Section -->
                <section id="dashboard-section" class="content-section active">
                    <h2><i class="fas fa-tachometer-alt"></i> Dashboard</h2>
                    <div class="stats-container">
                        <div class="stat-card">
                            <h3>Tổng tài sản</h3>
                            <p id="total-assets">0</p>
                        </div>
                        <div class="stat-card">
                            <h3>Tổng văn bản</h3>
                            <p id="total-documents">0</p>
                        </div>
                        <div class="stat-card">
                            <h3>Tài sản cần bảo trì</h3>
                            <p id="maintenance-needed">0</p>
                        </div>
                    </div>
                    <div class="recent-activity">
                        <h3>Hoạt động gần đây</h3>
                        <ul id="activity-list">
                            <!-- Activities will be populated by JS -->
                        </ul>
                    </div>
                </section>

                <!-- Assets Management Section -->
                <section id="assets-section" class="content-section">
                    <div class="section-header">
                        <h2><i class="fas fa-laptop"></i> Quản lý Tài sản CNTT</h2>
                        <button id="add-asset-btn" class="btn btn-primary"><i class="fas fa-plus"></i> Thêm tài sản</button>
                    </div>
                    <div class="search-filter">
                        <input type="text" id="asset-search" placeholder="Tìm kiếm tài sản...">
                        <select id="asset-filter">
                            <option value="all">Tất cả</option>
                            <option value="computer">Máy tính</option>
                            <option value="printer">Máy in</option>
                            <option value="network">Thiết bị mạng</option>
                            <option value="other">Khác</option>
                        </select>
                    </div>
                    <table id="assets-table" class="data-table">
                        <thead>
                            <tr>
                                <th>Mã tài sản</th>
                                <th>Tên thiết bị</th>
                                <th>Loại</th>
                                <th>Ngày mua</th>
                                <th>Giá trị</th>
                                <th>Trạng thái</th>
                                <th>Hành động</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Assets will be populated by JS -->
                        </tbody>
                    </table>
                </section>

                <!-- Documents Management Section -->
                <section id="documents-section" class="content-section">
                    <div class="section-header">
                        <h2><i class="fas fa-file-alt"></i> Quản lý Văn bản lưu trữ</h2>
                        <button id="add-document-btn" class="btn btn-primary"><i class="fas fa-plus"></i> Thêm văn bản</button>
                    </div>
                    <div class="search-filter">
                        <input type="text" id="document-search" placeholder="Tìm kiếm văn bản...">
                        <select id="document-filter">
                            <option value="all">Tất cả</option>
                            <option value="policy">Chính sách</option>
                            <option value="contract">Hợp đồng</option>
                            <option value="report">Báo cáo</option>
                            <option value="other">Khác</option>
                        </select>
                    </div>
                    <table id="documents-table" class="data-table">
                        <thead>
                            <tr>
                                <th>Mã văn bản</th>
                                <th>Tên văn bản</th>
                                <th>Loại</th>
                                <th>Ngày tạo</th>
                                <th>Người tạo</th>
                                <th>Mức độ bảo mật</th>
                                <th>Hành động</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Documents will be populated by JS -->
                        </tbody>
                    </table>
                </section>

                <!-- User Management Section (Admin only) -->
                <section id="users-section" class="content-section">
                    <div class="section-header">
                        <h2><i class="fas fa-users-cog"></i> Quản lý Người dùng</h2>
                        <button id="add-user-btn" class="btn btn-primary"><i class="fas fa-plus"></i> Thêm người dùng</button>
                    </div>
                    <table id="users-table" class="data-table">
                        <thead>
                            <tr>
                                <th>Tên đăng nhập</th>
                                <th>Họ tên</th>
                                <th>Email</th>
                                <th>Vai trò</th>
                                <th>Trạng thái</th>
                                <th>Hành động</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Users will be populated by JS -->
                        </tbody>
                    </table>
                </section>

                <!-- Reports Section -->
                <section id="reports-section" class="content-section">
                    <h2><i class="fas fa-chart-bar"></i> Báo cáo</h2>
                    <div class="report-options">
                        <div class="report-card" id="asset-report">
                            <i class="fas fa-laptop"></i>
                            <h3>Báo cáo tài sản</h3>
                        </div>
                        <div class="report-card" id="document-report">
                            <i class="fas fa-file-alt"></i>
                            <h3>Báo cáo văn bản</h3>
                        </div>
                        <div class="report-card" id="user-activity-report">
                            <i class="fas fa-user-clock"></i>
                            <h3>Hoạt động người dùng</h3>
                        </div>
                    </div>
                    <div id="report-results" class="report-results">
                        <!-- Report results will be displayed here -->
                    </div>
                </section>
            </main>
        </div>

        <!-- Modal for adding/editing assets -->
        <div id="asset-modal" class="modal">
            <div class="modal-content">
                <span class="close">&times;</span>
                <h2 id="asset-modal-title">Thêm tài sản mới</h2>
                <form id="asset-form">
                    <input type="hidden" id="asset-id">
                    <div class="form-group">
                        <label for="asset-name">Tên thiết bị:</label>
                        <input type="text" id="asset-name" required>
                    </div>
                    <div class="form-group">
                        <label for="asset-type">Loại thiết bị:</label>
                        <select id="asset-type" required>
                            <option value="computer">Máy tính</option>
                            <option value="printer">Máy in</option>
                            <option value="network">Thiết bị mạng</option>
                            <option value="other">Khác</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="asset-serial">Số serial:</label>
                        <input type="text" id="asset-serial">
                    </div>
                    <div class="form-group">
                        <label for="asset-purchase-date">Ngày mua:</label>
                        <input type="date" id="asset-purchase-date" required>
                    </div>
                    <div class="form-group">
                        <label for="asset-value">Giá trị (VND):</label>
                        <input type="number" id="asset-value" required>
                    </div>
                    <div class="form-group">
                        <label for="asset-status">Trạng thái:</label>
                        <select id="asset-status" required>
                            <option value="active">Đang hoạt động</option>
                            <option value="maintenance">Cần bảo trì</option>
                            <option value="retired">Đã thanh lý</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="asset-notes">Ghi chú:</label>
                        <textarea id="asset-notes" rows="3"></textarea>
                    </div>
                    <button type="submit" class="btn btn-primary">Lưu</button>
                </form>
            </div>
        </div>

        <!-- Modal for adding/editing documents -->
        <div id="document-modal" class="modal">
            <div class="modal-content">
                <span class="close">&times;</span>
                <h2 id="document-modal-title">Thêm văn bản mới</h2>
                <form id="document-form">
                    <input type="hidden" id="document-id">
                    <div class="form-group">
                        <label for="document-name">Tên văn bản:</label>
                        <input type="text" id="document-name" required>
                    </div>
                    <div class="form-group">
                        <label for="document-type">Loại văn bản:</label>
                        <select id="document-type" required>
                            <option value="policy">Chính sách</option>
                            <option value="contract">Hợp đồng</option>
                            <option value="report">Báo cáo</option>
                            <option value="other">Khác</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="document-security">Mức độ bảo mật:</label>
                        <select id="document-security" required>
                            <option value="public">Công khai</option>
                            <option value="internal">Nội bộ</option>
                            <option value="confidential">Bảo mật</option>
                            <option value="secret">Tối mật</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="document-file">Tệp đính kèm:</label>
                        <input type="file" id="document-file">
                    </div>
                    <div class="form-group">
                        <label for="document-notes">Mô tả:</label>
                        <textarea id="document-notes" rows="3" required></textarea>
                    </div>
                    <button type="submit" class="btn btn-primary">Lưu</button>
                </form>
            </div>
        </div>

        <!-- Modal for adding/editing users -->
        <div id="user-modal" class="modal">
            <div class="modal-content">
                <span class="close">&times;</span>
                <h2 id="user-modal-title">Thêm người dùng mới</h2>
                <form id="user-form">
                    <input type="hidden" id="user-id">
                    <div class="form-group">
                        <label for="user-username">Tên đăng nhập:</label>
                        <input type="text" id="user-username" required>
                    </div>
                    <div class="form-group">
                        <label for="user-password">Mật khẩu:</label>
                        <input type="password" id="user-password" required>
                    </div>
                    <div class="form-group">
                        <label for="user-fullname">Họ tên:</label>
                        <input type="text" id="user-fullname" required>
                    </div>
                    <div class="form-group">
                        <label for="user-email">Email:</label>
                        <input type="email" id="user-email" required>
                    </div>
                    <div class="form-group">
                        <label for="user-role">Vai trò:</label>
                        <select id="user-role" required>
                            <option value="admin">Quản trị viên</option>
                            <option value="manager">Quản lý</option>
                            <option value="staff">Nhân viên</option>
                            <option value="viewer">Người xem</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="user-status">Trạng thái:</label>
                        <select id="user-status" required>
                            <option value="active">Hoạt động</option>
                            <option value="inactive">Không hoạt động</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Quyền truy cập:</label>
                        <div class="permissions">
                            <label><input type="checkbox" name="permission" value="asset_read"> Xem tài sản</label>
                            <label><input type="checkbox" name="permission" value="asset_write"> Thêm/sửa tài sản</label>
                            <label><input type="checkbox" name="permission" value="asset_delete"> Xóa tài sản</label>
                            <label><input type="checkbox" name="permission" value="document_read"> Xem văn bản</label>
                            <label><input type="checkbox" name="permission" value="document_write"> Thêm/sửa văn bản</label>
                            <label><input type="checkbox" name="permission" value="document_delete"> Xóa văn bản</label>
                            <label><input type="checkbox" name="permission" value="user_manage"> Quản lý người dùng</label>
                        </div>
                    </div>
                    <button type="submit" class="btn btn-primary">Lưu</button>
                </form>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
