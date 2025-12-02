<html lang="th">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>แอปเช็คชื่อนักเรียน</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Sarabun', 'Noto Sans Thai', sans-serif;
      height: 100%;
      width: 100%;
    }
    
    html {
      height: 100%;
      width: 100%;
    }
    
    .app-wrapper {
      width: 100%;
      min-height: 100%;
    }
    
    .toast {
      position: fixed;
      top: 20px;
      right: 20px;
      padding: 16px 24px;
      border-radius: 8px;
      color: white;
      font-weight: 500;
      z-index: 1000;
      animation: slideIn 0.3s ease-out;
    }
    
    @keyframes slideIn {
      from {
        transform: translateX(400px);
        opacity: 0;
      }
      to {
        transform: translateX(0);
        opacity: 1;
      }
    }
    
    .loading-spinner {
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      border-top: 3px solid white;
      width: 20px;
      height: 20px;
      animation: spin 1s linear infinite;
      display: inline-block;
      margin-left: 8px;
    }
    
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="/_sdk/element_sdk.js" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-wrapper" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
   <div class="container mx-auto px-4 py-8" style="max-width: 1200px;"><!-- Welcome Screen -->
    <div id="welcome-screen" class="text-center">
     <div class="bg-white rounded-3xl shadow-2xl p-12 mb-6 max-w-3xl mx-auto"><!-- School Logo -->
      <div class="mb-6"><img src="http://www.pratoochai.ac.th/_files/webconfig/14100794_0_. .png" alt="ตราโรงเรียนประตูชัย" class="mx-auto" style="width: 120px; height: 120px; object-fit: contain;" onerror="this.style.display='none'; this.alt='ไม่สามารถโหลดตราโรงเรียนได้';">
      </div><!-- Welcome Illustration -->
      <div class="mb-8">
       <svg class="mx-auto" width="280" height="280" viewbox="0 0 280 280" fill="none" xmlns="http://www.w3.org/2000/svg"><!-- Cloud decorations --> <ellipse cx="60" cy="70" rx="25" ry="18" fill="#E0F2FE" opacity="0.6" /> <ellipse cx="220" cy="60" rx="30" ry="20" fill="#FCE7F3" opacity="0.6" /> <ellipse cx="200" cy="200" rx="28" ry="19" fill="#E0F2FE" opacity="0.5" /> <!-- School building --> <rect x="80" y="140" width="120" height="90" rx="8" fill="#FCA5A5" /> <rect x="130" y="170" width="20" height="30" fill="#FEF3C7" /> <rect x="95" y="160" width="18" height="18" fill="#DBEAFE" /> <rect x="167" y="160" width="18" height="18" fill="#DBEAFE" /> <rect x="95" y="190" width="18" height="18" fill="#DBEAFE" /> <rect x="167" y="190" width="18" height="18" fill="#DBEAFE" /> <!-- Roof --> <path d="M 70 140 L 140 100 L 210 140" fill="#F472B6" stroke="#EC4899" stroke-width="3" /> <circle cx="140" cy="95" r="8" fill="#FDE047" /> <!-- Teacher figure --> <circle cx="140" cy="240" r="12" fill="#FBD5D5" /> <rect x="133" y="252" width="14" height="20" rx="3" fill="#FBCFE8" /> <!-- Stars decoration --> <text x="40" y="120" font-size="24" fill="#FCD34D">
         ⭐
        </text> <text x="230" y="140" font-size="20" fill="#FCD34D">
         ✨
        </text> <text x="50" y="210" font-size="18" fill="#FCD34D">
         ⭐
        </text> <!-- Books --> <rect x="30" y="200" width="15" height="20" rx="2" fill="#FBCFE8" /> <rect x="240" y="190" width="15" height="25" rx="2" fill="#BFDBFE" />
       </svg>
      </div>
      <h1 id="app-title" class="font-bold mb-4" style="background: linear-gradient(135deg, #EC4899 0%, #8B5CF6 50%, #3B82F6 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; line-height: 1.6; font-size: 1.3rem;">ระบบเช็คการมาเรียน นักเรียน MEP โรงเรียนประตูชัย<br>
        สำนักงานเขตพื้นที่การศึกษาประถมศึกษาพระนครศรีอยุธยา เขต 1</h1>
      <div class="inline-block p-4 bg-pink-50 rounded-2xl mb-8">
       <p class="text-pink-600 font-medium">📚 กรุณาเลือกห้องเรียนเพื่อเริ่มเช็คชื่อ</p>
      </div><!-- Classroom Selection Grid -->
      <div class="grid grid-cols-2 md:grid-cols-3 gap-4 max-w-2xl mx-auto"><button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-pink-100 to-pink-200 hover:from-pink-200 hover:to-pink-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.1/5">
        <div class="text-5xl mb-2">
         🐠
        </div>
        <div class="text-xl font-bold text-pink-700">
         ป.1/5
        </div></button> <button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-blue-100 to-blue-200 hover:from-blue-200 hover:to-blue-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.2/5">
        <div class="text-5xl mb-2">
         🐻
        </div>
        <div class="text-xl font-bold text-blue-700">
         ป.2/5
        </div></button> <button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-purple-100 to-purple-200 hover:from-purple-200 hover:to-purple-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.3/5">
        <div class="text-5xl mb-2">
         🦊
        </div>
        <div class="text-xl font-bold text-purple-700">
         ป.3/5
        </div></button> <button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-pink-100 to-purple-200 hover:from-pink-200 hover:to-purple-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.4/5">
        <div class="text-5xl mb-2">
         🦁
        </div>
        <div class="text-xl font-bold text-pink-700">
         ป.4/5
        </div></button> <button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-blue-100 to-purple-200 hover:from-blue-200 hover:to-purple-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.5/5">
        <div class="text-5xl mb-2">
         🐰
        </div>
        <div class="text-xl font-bold text-blue-700">
         ป.5/5
        </div></button> <button class="classroom-select-btn group relative overflow-hidden bg-gradient-to-br from-purple-100 to-pink-200 hover:from-purple-200 hover:to-pink-300 p-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:scale-105" data-classroom="ป.6/5">
        <div class="text-5xl mb-2">
         🐯
        </div>
        <div class="text-xl font-bold text-purple-700">
         ป.6/5
        </div></button>
      </div>
     </div>
    </div><!-- Attendance Screen (Hidden initially) -->
    <div id="attendance-screen" style="display: none;">
     <header class="text-center mb-6"><button id="back-to-menu" class="inline-flex items-center gap-2 bg-white text-purple-600 px-4 py-2 rounded-lg font-medium hover:bg-purple-50 transition-colors mb-4"> <span>←</span> กลับหน้าหลัก </button>
      <h1 class="text-3xl font-bold text-white mb-2">เช็คชื่อ <span id="current-classroom-title"></span></h1>
      <p id="buddhist-date-display" class="text-white text-opacity-90 text-lg font-medium"></p>
     </header><!-- Main Content -->
     <main class="bg-white rounded-2xl shadow-2xl p-6 mb-6"><!-- Add Student Form -->
      <div class="bg-purple-50 rounded-xl p-4 mb-6">
       <h2 class="text-xl font-bold text-gray-800 mb-4">เพิ่มนักเรียน</h2>
       <form id="add-student-form" class="flex flex-wrap gap-3">
        <div class="flex-1 min-w-[200px]"><label for="student-name-input" class="block text-sm font-medium text-gray-700 mb-1">ชื่อนักเรียน</label> <input type="text" id="student-name-input" placeholder="กรอกชื่อนักเรียน" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
        </div>
        <div class="flex items-end"><button type="submit" id="add-student-btn" class="px-6 py-2 bg-purple-600 text-white rounded-lg font-medium hover:bg-purple-700 transition-colors disabled:opacity-50 disabled:cursor-not-allowed"> เพิ่มนักเรียน </button>
        </div>
       </form>
      </div><!-- Date Filter -->
      <div class="flex flex-wrap items-center gap-3 mb-4"><label for="date-filter" class="font-medium text-gray-700">เลือกวันที่:</label> <input type="date" id="date-filter" class="px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500"> <button id="today-btn" class="px-4 py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors font-medium"> วันนี้ </button>
      </div><!-- Attendance List -->
      <div id="attendance-container">
       <h3 class="text-lg font-bold text-gray-800 mb-3">รายชื่อนักเรียน</h3>
       <div id="student-list" class="space-y-2">
        <p class="text-gray-500 text-center py-8">ยังไม่มีนักเรียนในห้องเรียนนี้</p>
       </div>
      </div><!-- Summary -->
      <div class="mt-6 p-4 bg-blue-50 rounded-xl">
       <h3 class="font-bold text-gray-800 mb-2">สรุปการมาเรียน</h3>
       <div class="grid grid-cols-3 gap-4 text-center">
        <div>
         <p class="text-2xl font-bold text-green-600" id="present-count">0</p>
         <p class="text-lg font-semibold text-green-700" id="present-percent">0%</p>
         <p class="text-sm text-gray-600">มาเรียน</p>
        </div>
        <div>
         <p class="text-2xl font-bold text-yellow-600" id="leave-count">0</p>
         <p class="text-lg font-semibold text-yellow-700" id="leave-percent">0%</p>
         <p class="text-sm text-gray-600">ลา</p>
        </div>
        <div>
         <p class="text-2xl font-bold text-red-600" id="sick-count">0</p>
         <p class="text-lg font-semibold text-red-700" id="sick-percent">0%</p>
         <p class="text-sm text-gray-600">ป่วย</p>
        </div>
       </div>
      </div>
     </main>
    </div><!-- Footer -->
    <footer class="text-center">
     <p id="footer-text" class="text-white text-opacity-80">จัดการการมาเรียนอย่างมีประสิทธิภาพ</p>
     <p class="text-white text-opacity-60 text-sm mt-2">พัฒนาโดย นางวิรัลพัชษ์ สว่างเดือน</p>
    </footer>
   </div>
  </div>
  <script>
    // LocalStorage keys
    const STORAGE_KEY = 'school_attendance_records';

    // Status constants
    const STATUS_PRESENT = 'present';
    const STATUS_LEAVE = 'leave';
    const STATUS_SICK = 'sick';

    let allRecords = [];
    let currentClassroom = "ป.1/5";
    let currentDate = new Date().toISOString().split('T')[0];

    // LocalStorage functions
    function loadFromLocalStorage() {
      try {
        const data = localStorage.getItem(STORAGE_KEY);
        return data ? JSON.parse(data) : [];
      } catch (e) {
        console.error('Error loading data:', e);
        return [];
      }
    }

    function saveToLocalStorage(records) {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(records));
      } catch (e) {
        console.error('Error saving data:', e);
        showToast('ไม่สามารถบันทึกข้อมูลได้', 'error');
      }
    }

    function generateId() {
      return Date.now().toString(36) + Math.random().toString(36).substr(2);
    }

    // Helper function to convert date to Buddhist Era display
    function toBuddhistYear(dateStr) {
      const date = new Date(dateStr);
      const buddhistYear = date.getFullYear() + 543;
      const thaiMonths = ['มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน', 
                          'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม'];
      const day = date.getDate();
      const month = thaiMonths[date.getMonth()];
      return `${day} ${month} ${buddhistYear}`;
    }

    function updateDateDisplay() {
      const displayEl = document.getElementById('buddhist-date-display');
      if (displayEl) {
        displayEl.textContent = `วันที่: ${toBuddhistYear(currentDate)}`;
      }
    }

    // Initialize app
    function initializeApp() {
      allRecords = loadFromLocalStorage();
      setupEventListeners();
      document.getElementById('date-filter').value = currentDate;
      updateDateDisplay();
      showWelcomeScreen();
    }

    function setupEventListeners() {
      // Classroom selection buttons
      document.querySelectorAll('.classroom-select-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          currentClassroom = btn.dataset.classroom;
          showAttendanceScreen();
        });
      });

      // Back to menu button
      document.getElementById('back-to-menu').addEventListener('click', () => {
        showWelcomeScreen();
      });

      // Add student form
      document.getElementById('add-student-form').addEventListener('submit', (e) => {
        e.preventDefault();
        
        const nameInput = document.getElementById('student-name-input');
        const studentName = nameInput.value.trim();
        
        if (!studentName) return;

        // Check if student already exists in this classroom
        const existingStudent = allRecords.find(r => 
          r.classroom === currentClassroom && r.student_name === studentName
        );
        
        if (existingStudent) {
          showToast('นักเรียนคนนี้มีอยู่แล้ว', 'error');
          return;
        }

        // Add new student
        const newRecord = {
          id: generateId(),
          student_name: studentName,
          classroom: currentClassroom,
          date: currentDate,
          status: STATUS_PRESENT,
          created_at: new Date().toISOString()
        };

        allRecords.push(newRecord);
        saveToLocalStorage(allRecords);
        
        nameInput.value = '';
        showToast('เพิ่มนักเรียนสำเร็จ', 'success');
        
        renderStudentList();
        updateSummary();
      });

      // Date filter
      document.getElementById('date-filter').addEventListener('change', (e) => {
        currentDate = e.target.value;
        renderStudentList();
        updateSummary();
        updateDateDisplay();
      });

      document.getElementById('today-btn').addEventListener('click', () => {
        currentDate = new Date().toISOString().split('T')[0];
        document.getElementById('date-filter').value = currentDate;
        renderStudentList();
        updateSummary();
        updateDateDisplay();
      });
    }

    function showWelcomeScreen() {
      document.getElementById('welcome-screen').style.display = 'block';
      document.getElementById('attendance-screen').style.display = 'none';
    }

    function showAttendanceScreen() {
      document.getElementById('welcome-screen').style.display = 'none';
      document.getElementById('attendance-screen').style.display = 'block';
      document.getElementById('current-classroom-title').textContent = currentClassroom;
      updateDateDisplay();
      renderStudentList();
      updateSummary();
    }

    function renderStudentList() {
      const container = document.getElementById('student-list');
      
      // Get all unique students in this classroom
      const studentsMap = new Map();
      allRecords.forEach(r => {
        if (r.classroom === currentClassroom) {
          if (!studentsMap.has(r.student_name)) {
            studentsMap.set(r.student_name, r.student_name);
          }
        }
      });

      const uniqueStudents = Array.from(studentsMap.keys());

      if (uniqueStudents.length === 0) {
        container.innerHTML = '<p class="text-gray-500 text-center py-8">ยังไม่มีนักเรียนในห้องเรียนนี้</p>';
        return;
      }

      container.innerHTML = '';

      uniqueStudents.forEach(studentName => {
        // Find record for this student on current date
        const todayRecord = allRecords.find(r => 
          r.classroom === currentClassroom && 
          r.student_name === studentName && 
          r.date === currentDate
        );

        container.appendChild(createStudentElement(studentName, todayRecord));
      });
    }

    function createStudentElement(studentName, record) {
      const div = document.createElement('div');
      div.dataset.studentName = studentName;
      if (record) {
        div.dataset.recordId = record.id;
      }
      div.className = 'flex items-center justify-between p-4 bg-gray-50 rounded-lg hover:bg-gray-100 transition-colors';
      
      updateStudentElement(div, studentName, record);
      return div;
    }

    function updateStudentElement(element, studentName, record) {
      const currentStatus = record ? record.status : STATUS_PRESENT;

      const nameDiv = document.createElement('div');
      nameDiv.className = 'flex-1';
      nameDiv.innerHTML = `
        <p class="font-medium text-gray-800">${studentName}</p>
        <p class="text-sm text-gray-500">${currentClassroom}</p>
      `;

      const buttonsDiv = document.createElement('div');
      buttonsDiv.className = 'flex items-center gap-2';

      // Create Present button
      const presentBtn = document.createElement('button');
      presentBtn.className = 'status-btn px-3 py-1 rounded-lg text-white text-sm font-medium bg-green-500';
      presentBtn.textContent = 'มาเรียน';
      presentBtn.dataset.status = STATUS_PRESENT;
      if (currentStatus === STATUS_PRESENT) {
        presentBtn.style.opacity = '1';
        presentBtn.style.transform = 'scale(1.05)';
      } else {
        presentBtn.style.opacity = '0.5';
      }

      // Create Leave button
      const leaveBtn = document.createElement('button');
      leaveBtn.className = 'status-btn px-3 py-1 rounded-lg text-white text-sm font-medium bg-yellow-500';
      leaveBtn.textContent = 'ลา';
      leaveBtn.dataset.status = STATUS_LEAVE;
      if (currentStatus === STATUS_LEAVE) {
        leaveBtn.style.opacity = '1';
        leaveBtn.style.transform = 'scale(1.05)';
      } else {
        leaveBtn.style.opacity = '0.5';
      }

      // Create Sick button
      const sickBtn = document.createElement('button');
      sickBtn.className = 'status-btn px-3 py-1 rounded-lg text-white text-sm font-medium bg-red-500';
      sickBtn.textContent = 'ป่วย';
      sickBtn.dataset.status = STATUS_SICK;
      if (currentStatus === STATUS_SICK) {
        sickBtn.style.opacity = '1';
        sickBtn.style.transform = 'scale(1.05)';
      } else {
        sickBtn.style.opacity = '0.5';
      }

      // Create Delete button
      const deleteBtn = document.createElement('button');
      deleteBtn.className = 'delete-btn px-3 py-1 bg-gray-300 text-gray-700 rounded-lg text-sm font-medium hover:bg-red-500 hover:text-white transition-colors';
      deleteBtn.textContent = 'ลบ';

      // Add event listeners for status buttons
      [presentBtn, leaveBtn, sickBtn].forEach(btn => {
        btn.addEventListener('click', () => {
          if (record) {
            // Update existing record
            const recordIndex = allRecords.findIndex(r => r.id === record.id);
            if (recordIndex !== -1) {
              allRecords[recordIndex].status = btn.dataset.status;
              saveToLocalStorage(allRecords);
              renderStudentList();
              updateSummary();
            }
          } else {
            // Create new record for this date
            const newRecord = {
              id: generateId(),
              student_name: studentName,
              classroom: currentClassroom,
              date: currentDate,
              status: btn.dataset.status,
              created_at: new Date().toISOString()
            };
            allRecords.push(newRecord);
            saveToLocalStorage(allRecords);
            renderStudentList();
            updateSummary();
          }
        });
      });

      // Delete button event listener
      deleteBtn.addEventListener('click', () => {
        // Delete ALL records of this student in this classroom
        const initialLength = allRecords.length;
        allRecords = allRecords.filter(r => 
          !(r.classroom === currentClassroom && r.student_name === studentName)
        );
        
        if (allRecords.length < initialLength) {
          saveToLocalStorage(allRecords);
          showToast('ลบนักเรียนสำเร็จ', 'success');
          renderStudentList();
          updateSummary();
        } else {
          showToast('ไม่มีข้อมูลให้ลบ', 'error');
        }
      });

      buttonsDiv.appendChild(presentBtn);
      buttonsDiv.appendChild(leaveBtn);
      buttonsDiv.appendChild(sickBtn);
      buttonsDiv.appendChild(deleteBtn);

      element.innerHTML = '';
      element.appendChild(nameDiv);
      element.appendChild(buttonsDiv);
    }

    function updateSummary() {
      const todayRecords = allRecords.filter(r => 
        r.classroom === currentClassroom && r.date === currentDate
      );

      const present = todayRecords.filter(r => r.status === STATUS_PRESENT).length;
      const leave = todayRecords.filter(r => r.status === STATUS_LEAVE).length;
      const sick = todayRecords.filter(r => r.status === STATUS_SICK).length;
      
      const total = todayRecords.length;
      const presentPercent = total > 0 ? Math.round((present / total) * 100) : 0;
      const leavePercent = total > 0 ? Math.round((leave / total) * 100) : 0;
      const sickPercent = total > 0 ? Math.round((sick / total) * 100) : 0;

      document.getElementById('present-count').textContent = present;
      document.getElementById('leave-count').textContent = leave;
      document.getElementById('sick-count').textContent = sick;
      
      document.getElementById('present-percent').textContent = presentPercent + '%';
      document.getElementById('leave-percent').textContent = leavePercent + '%';
      document.getElementById('sick-percent').textContent = sickPercent + '%';
    }

    function showToast(message, type) {
      const toast = document.createElement('div');
      toast.className = 'toast';
      toast.textContent = message;
      toast.style.backgroundColor = type === 'success' ? '#10b981' : '#ef4444';
      
      document.body.appendChild(toast);
      
      setTimeout(() => {
        toast.remove();
      }, 3000);
    }

    // Start the app
    initializeApp();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a7b03fed4778960',t:'MTc2NDY4MDUxNC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
