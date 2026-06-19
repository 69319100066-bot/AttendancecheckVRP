<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบเช็คชื่อเข้าเรียน</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/lucide@latest"></script>
</head>
<body>
    <div id="app"></div>

    <script>
        // ข้อมูลสาขาวิชา แยกตามระดับชั้น
        const VOCATIONAL_BRANCHES = [
            "ช่างยนต์", "ช่างกลโรงงาน", "ช่างไฟฟ้ากำลัง", "อิเล็กทรอนิกส์",
            "ช่างก่อสร้าง", "สถาปัตยกรรม", "การบัญชี", "การตลาด",
            "คอมพิวเตอร์ธุรกิจ", "เทคโนโลยีสารสนเทศ"
        ];

        const HIGH_VOCATIONAL_BRANCHES = [
            "เทคนิคยานยนต์", "เทคนิคการผลิต", "ไฟฟ้ากำลัง", "อิเล็กทรอนิกส์อุตสาหกรรม",
            "ช่างโยธา", "เทคนิคสถาปัตยกรรม", "การบัญชี", "การตลาด",
            "เทคโนโลยีธุรกิจดิจิทัล", "นักพัฒนาซอฟต์แวร์"
        ];

        // State
        let formData = {
            studentId: '',
            fullName: '',
            level: '',
            branch: ''
        };

        let records = [];
        let showSuccess = false;

        // ฟังก์ชันจัดการการเปลี่ยนแปลง Input
        function handleInputChange(e) {
            const { name, value } = e.target;

            if (name === 'level') {
                formData = { ...formData, [name]: value, branch: '' };
            } else {
                formData = { ...formData, [name]: value };
            }

            updateUI();
        }

        // ฟังก์ชันส่งฟอร์ม
        function handleSubmit(e) {
            e.preventDefault();

            // ตรวจสอบว่ากรอกข้อมูลครบหรือไม่
            if (!formData.studentId || !formData.fullName || !formData.level || !formData.branch) {
                alert('กรุณากรอกข้อมูลให้ครบถ้วน');
                return;
            }

            const now = new Date();

            // จัดรูปแบบวันที่
            const dateOptions = { year: 'numeric', month: 'short', day: 'numeric' };
            const formattedDate = now.toLocaleDateString('th-TH', dateOptions);

            // จัดรูปแบบเวลา
            const formattedTime = now.toLocaleTimeString('th-TH') + ' น.';

            // สร้างออบเจกต์ข้อมูลใหม่
            const newRecord = {
                id: Date.now(),
                ...formData,
                date: formattedDate,
                time: formattedTime,
                timestamp: now
            };

            // เพิ่มข้อมูลใหม่ลงในประวัติ
            records = [newRecord, ...records];

            // แสดงข้อความสำเร็จ
            showSuccess = true;
            updateUI();

            setTimeout(() => {
                showSuccess = false;
                updateUI();
            }, 3000);

            // ล้างข้อมูลในฟอร์ม
            formData = {
                studentId: '',
                fullName: '',
                level: '',
                branch: ''
            };

            updateUI();
        }

        // ฟังก์ชันเลือกสาขาวิชาตามระดับชั้น
        function getCurrentBranches() {
            if (formData.level === 'ปวช') return VOCATIONAL_BRANCHES;
            if (formData.level === 'ปวส') return HIGH_VOCATIONAL_BRANCHES;
            return [];
        }

        // ฟังก์ชันอัพเดต UI
        function updateUI() {
            const currentBranches = getCurrentBranches();

            const html = `
                <div class="min-h-screen bg-slate-50 py-8 px-4 font-sans text-slate-800">
                    <div class="max-w-4xl mx-auto space-y-8">
                        
                        <!-- ส่วนหัวกระดาษ (Header) -->
                        <div class="text-center space-y-2">
                            <h1 class="text-3xl font-bold text-blue-700 flex items-center justify-center gap-2">
                                <svg class="w-8 h-8" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08v.02a10 10 0 1 1-5.93-9.14"></path><polyline points="22 4 12 14.01 9 11.01"></polyline></svg>
                                ระบบเช็คชื่อเข้าเรียน
                            </h1>
                            <p class="text-slate-500">กรุณากรอกข้อมูลเพื่อบันทึกเวลาเข้าเรียนของคุณ</p>
                        </div>

                        <!-- ส่วนฟอร์มกรอกข้อมูล -->
                        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 md:p-8 relative overflow-hidden">
                            <!-- แจ้งเตือนเมื่อบันทึกสำเร็จ -->
                            ${showSuccess ? `
                                <div class="absolute top-0 left-0 right-0 bg-green-500 text-white text-center py-2 font-medium animate-pulse">
                                    บันทึกข้อมูลสำเร็จ!
                                </div>
                            ` : ''}

                            <form onsubmit="handleSubmit(event)" class="space-y-6 mt-4">
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                    
                                    <!-- รหัสนักศึกษา -->
                                    <div class="space-y-2">
                                        <label class="flex items-center gap-2 text-sm font-semibold text-slate-700">
                                            <svg class="w-4 h-4 text-blue-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" y1="9" x2="20" y2="9"></line><line x1="4" y1="15" x2="20" y2="15"></line><line x1="10" y1="3" x2="8" y2="21"></line><line x1="16" y1="3" x2="14" y2="21"></line></svg>
                                            รหัสนักศึกษา
                                        </label>
                                        <input
                                            type="text"
                                            name="studentId"
                                            value="${formData.studentId}"
                                            onchange="handleInputChange(event)"
                                            placeholder="เช่น 65201010001"
                                            class="w-full px-4 py-3 rounded-lg border border-slate-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors"
                                            required
                                        />
                                    </div>

                                    <!-- ชื่อ-นามสกุล -->
                                    <div class="space-y-2">
                                        <label class="flex items-center gap-2 text-sm font-semibold text-slate-700">
                                            <svg class="w-4 h-4 text-blue-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>
                                            ชื่อ-นามสกุล
                                        </label>
                                        <input
                                            type="text"
                                            name="fullName"
                                            value="${formData.fullName}"
                                            onchange="handleInputChange(event)"
                                            placeholder="นาย/นางสาว..."
                                            class="w-full px-4 py-3 rounded-lg border border-slate-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors"
                                            required
                                        />
                                    </div>

                                    <!-- ระดับชั้น -->
                                    <div class="space-y-2">
                                        <label class="flex items-center gap-2 text-sm font-semibold text-slate-700">
                                            <svg class="w-4 h-4 text-blue-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 10v6m0 0v6m0-6H2m0 0v6m0-6V4"></path></svg>
                                            ระดับชั้น
                                        </label>
                                        <div class="grid grid-cols-2 gap-4">
                                            <label class="flex items-center justify-center gap-2 px-4 py-3 rounded-lg border cursor-pointer transition-all ${formData.level === 'ปวช' ? 'bg-blue-50 border-blue-500 text-blue-700 shadow-sm' : 'border-slate-300 hover:bg-slate-50'}">
                                                <input
                                                    type="radio"
                                                    name="level"
                                                    value="ปวช"
                                                    ${formData.level === 'ปวช' ? 'checked' : ''}
                                                    onchange="handleInputChange(event)"
                                                    class="hidden"
                                                />
                                                <span class="font-medium">ปวช.</span>
                                            </label>
                                            <label class="flex items-center justify-center gap-2 px-4 py-3 rounded-lg border cursor-pointer transition-all ${formData.level === 'ปวส' ? 'bg-blue-50 border-blue-500 text-blue-700 shadow-sm' : 'border-slate-300 hover:bg-slate-50'}">
                                                <input
                                                    type="radio"
                                                    name="level"
                                                    value="ปวส"
                                                    ${formData.level === 'ปวส' ? 'checked' : ''}
                                                    onchange="handleInputChange(event)"
                                                    class="hidden"
                                                />
                                                <span class="font-medium">ปวส.</span>
                                            </label>
                                        </div>
                                    </div>

                                    <!-- สาขาวิชา -->
                                    <div class="space-y-2">
                                        <label class="flex items-center gap-2 text-sm font-semibold text-slate-700">
                                            <svg class="w-4 h-4 text-blue-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"></path><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"></path></svg>
                                            สาขาวิชา
                                        </label>
                                        <select
                                            name="branch"
                                            value="${formData.branch}"
                                            onchange="handleInputChange(event)"
                                            ${!formData.level ? 'disabled' : ''}
                                            class="${!formData.level ? 'bg-slate-100 border-slate-200 text-slate-400 cursor-not-allowed' : 'border-slate-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white'} w-full px-4 py-3 rounded-lg border transition-colors"
                                            required
                                        >
                                            <option value="">
                                                ${!formData.level ? 'กรุณาเลือกระดับชั้นก่อน' : 'เลือกสาขาวิชา...'}
                                            </option>
                                            ${currentBranches.map(branch => `<option value="${branch}">${branch}</option>`).join('')}
                                        </select>
                                    </div>

                                </div>

                                <button
                                    type="submit"
                                    class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-lg shadow-md transition-transform transform active:scale-[0.98] flex justify-center items-center gap-2"
                                >
                                    <svg class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08v.02a10 10 0 1 1-5.93-9.14"></path><polyline points="22 4 12 14.01 9 11.01"></polyline></svg>
                                    บันทึกการเข้าเรียน
                                </button>
                            </form>
                        </div>

                        <!-- ส่วนแสดงประวัติการเช็คชื่อ -->
                        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 md:p-8">
                            <div class="flex items-center justify-between mb-6">
                                <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2">
                                    <svg class="w-6 h-6 text-slate-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3.01" y2="6"></line><line x1="3" y1="12" x2="3.01" y2="12"></line><line x1="3" y1="18" x2="3.01" y2="18"></line></svg>
                                    ประวัติการเช็คชื่อวันนี้
                                </h2>
                                <div class="bg-blue-100 text-blue-800 text-sm font-semibold px-3 py-1 rounded-full">
                                    รวม ${records.length} รายการ
                                </div>
                            </div>

                            ${records.length === 0 ? `
                                <div class="text-center py-12 text-slate-400 bg-slate-50 rounded-xl border border-dashed border-slate-300">
                                    ยังไม่มีข้อมูลการเช็คชื่อ
                                </div>
                            ` : `
                                <div class="overflow-x-auto">
                                    <table class="w-full text-left text-sm whitespace-nowrap">
                                        <thead class="bg-slate-50 text-slate-600 border-b border-slate-200">
                                            <tr>
                                                <th class="px-4 py-3 font-semibold rounded-tl-lg">วันที่</th>
                                                <th class="px-4 py-3 font-semibold">เวลา</th>
                                                <th class="px-4 py-3 font-semibold">รหัสนักศึกษา</th>
                                                <th class="px-4 py-3 font-semibold">ชื่อ-นามสกุล</th>
                                                <th class="px-4 py-3 font-semibold">ระดับ/สาขา</th>
                                            </tr>
                                        </thead>
                                        <tbody class="divide-y divide-slate-100">
                                            ${records.map(record => `
                                                <tr class="hover:bg-slate-50 transition-colors">
                                                    <td class="px-4 py-3">
                                                        <div class="flex items-center gap-1.5 text-slate-600">
                                                            <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect><line x1="16" y1="2" x2="16" y2="6"></line><line x1="8" y1="2" x2="8" y2="6"></line><line x1="3" y1="10" x2="21" y2="10"></line></svg>
                                                            ${record.date}
                                                        </div>
                                                    </td>
                                                    <td class="px-4 py-3">
                                                        <div class="flex items-center gap-1.5 font-medium text-blue-600">
                                                            <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
                                                            ${record.time}
                                                        </div>
                                                    </td>
                                                    <td class="px-4 py-3 font-mono text-slate-700">${record.studentId}</td>
                                                    <td class="px-4 py-3 font-medium text-slate-900">${record.fullName}</td>
                                                    <td class="px-4 py-3 text-slate-600">
                                                        <span class="${record.level === 'ปวช' ? 'bg-indigo-100 text-indigo-800' : 'bg-purple-100 text-purple-800'} inline-flex items-center px-2 py-0.5 rounded text-xs font-medium mr-2">
                                                            ${record.level}
                                                        </span>
                                                        ${record.branch}
                                                    </td>
                                                </tr>
                                            `).join('')}
                                        </tbody>
                                    </table>
                                </div>
                            `}
                        </div>

                    </div>
                </div>
            `;

            document.getElementById('app').innerHTML = html;
        }

        // เรียก updateUI ครั้งแรก
        updateUI();
    </script>
</body>
</html>
