<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-800 via-slate-700 to-slate-900 py-8 px-4 sm:px-6 lg:px-8">
    <div class="max-w-5xl mx-auto">
      <!-- Logo 與標題區 -->
      <div class="text-center mb-8">
        <div class="mb-6">
          <img src="/logo.png" alt="Logo" class="mx-auto h-24 md:h-32 w-auto object-contain">
        </div>
        <h1 class="text-3xl md:text-4xl font-bold text-white mb-2">資金需求申請表</h1>
        <p class="text-slate-300">請詳細填寫以下資料，我們將儘速為您處理</p>
      </div>

      <!-- 成功訊息 -->
      <div v-if="submitted" class="bg-white rounded-lg shadow-2xl p-12 text-center">
        <div class="mb-6">
          <img src="/logo.png" alt="Logo" class="mx-auto h-20 w-auto object-contain opacity-50">
        </div>
        <div class="text-green-500 text-6xl mb-4">✓</div>
        <h2 class="text-3xl font-bold text-slate-800 mb-2">申請已送出</h2>
        <p class="text-slate-600">我們已收到您的申請，將盡快與您聯繫</p>
      </div>

      <!-- 表單 -->
      <form v-else @submit.prevent="handleSubmit" class="bg-white rounded-lg shadow-2xl p-6 md:p-8">
        <!-- 基本資料 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">基本資料</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">姓名 *</label>
              <input v-model="form.name" type="text" required 
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">年齡</label>
              <input v-model="form.age" type="number" min="18" max="100"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">學歷</label>
              <select v-model="form.education"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="國中">國中</option>
                <option value="高中職">高中職</option>
                <option value="專科">專科</option>
                <option value="大學">大學</option>
                <option value="碩士">碩士</option>
                <option value="博士">博士</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">出生年月日</label>
              <div class="grid grid-cols-3 gap-2">
                <input v-model="form.birthYear" type="number" placeholder="年" min="1900" max="2025"
                  class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <input v-model="form.birthMonth" type="number" placeholder="月" min="1" max="12"
                  class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <input v-model="form.birthDay" type="number" placeholder="日" min="1" max="31"
                  class="px-3 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
              </div>
            </div>
            <div class="md:col-span-2">
              <label class="block text-sm font-semibold text-slate-700 mb-2">手機號碼 *</label>
              <input v-model="form.phone" type="tel" required pattern="[0-9]{10}"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
          </div>
        </div>

        <!-- 戶籍資訊 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">戶籍資訊</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="md:col-span-2">
              <label class="block text-sm font-semibold text-slate-700 mb-2">戶籍地</label>
              <input v-model="form.registeredAddress" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">戶籍地電話</label>
              <input v-model="form.registeredPhone" type="tel"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">戶籍地誰的房子</label>
              <input v-model="form.registeredHouseOwner" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
          </div>
        </div>

        <!-- 通訊資訊 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">通訊資訊</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="md:col-span-2">
              <label class="block text-sm font-semibold text-slate-700 mb-2">通訊地</label>
              <input v-model="form.mailingAddress" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">通訊地電話</label>
              <input v-model="form.mailingPhone" type="tel"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">通訊地誰的房子</label>
              <input v-model="form.mailingHouseOwner" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
          </div>
        </div>

        <!-- 工作資訊 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">工作資訊</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">工作性質</label>
              <select v-model="form.jobType"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="全職">全職</option>
                <option value="兼職">兼職</option>
                <option value="自營">自營</option>
                <option value="無業">無業</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">目前工作做多久</label>
              <input v-model="form.jobDuration" type="text" placeholder="例：2年3個月"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">目前薪資 *</label>
              <input v-model="form.salary" type="number" required min="0"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無薪轉</label>
              <select v-model="form.hasSalaryTransfer"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無勞保</label>
              <select v-model="form.hasLaborInsurance"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">公司名稱</label>
              <input v-model="form.companyName" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div class="md:col-span-2">
              <label class="block text-sm font-semibold text-slate-700 mb-2">公司地址</label>
              <input v-model="form.companyAddress" type="text"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">公司電話</label>
              <input v-model="form.companyPhone" type="tel"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
          </div>
        </div>

        <!-- 資產與信用 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">資產與信用</h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無駕照</label>
              <select v-model="form.hasDriverLicense"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無保人</label>
              <select v-model="form.hasGuarantor"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無存款</label>
              <select v-model="form.hasSavings"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">存款大約多少</label>
              <input v-model="form.savingsAmount" type="text" placeholder="例：10萬"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">有無信用卡</label>
              <select v-model="form.hasCreditCard"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="有">有</option>
                <option value="無">無</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">信用正常嗎</label>
              <select v-model="form.creditNormal"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="正常">正常</option>
                <option value="有瑕疵">有瑕疵</option>
              </select>
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">平均每個月刷多少</label>
              <input v-model="form.monthlyCardSpending" type="number" min="0"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
            </div>
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">信用卡還款方式</label>
              <select v-model="form.cardPaymentMethod"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                <option value="">請選擇</option>
                <option value="全額繳清">全額繳清</option>
                <option value="最低">最低</option>
              </select>
            </div>
          </div>
        </div>

        <!-- 貸款往來 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">貸款往來</h2>
          <div class="grid grid-cols-1 gap-6">
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">銀行/融資往來紀錄</label>
              <textarea v-model="form.loanHistory" rows="3"
                placeholder="例：信貸、房貸、學貸、車貸、機車貸、商品分期等"
                class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent"></textarea>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">已繳幾期</label>
                <input v-model="form.paidInstallments" type="text"
                  class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
              </div>
              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">是否有正常繳款</label>
                <select v-model="form.paymentNormal"
                  class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
                  <option value="">請選擇</option>
                  <option value="是">是</option>
                  <option value="否">否</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">當初貸款金額</label>
                <input v-model="form.loanAmount" type="number" min="0"
                  class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
              </div>
              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">貸款銀行名稱</label>
                <input v-model="form.loanBankName" type="text"
                  class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent">
              </div>
            </div>
          </div>
        </div>

        <!-- 其他 -->
        <div class="mb-8">
          <h2 class="text-2xl font-bold text-slate-800 mb-4 pb-2 border-b-2 border-blue-900">其他</h2>
          <div>
            <label class="block text-sm font-semibold text-slate-700 mb-2">名下有無動產與不動產</label>
            <textarea v-model="form.assets" rows="3"
              placeholder="請說明您名下的動產（如車輛）或不動產（如房屋、土地）"
              class="w-full px-4 py-2 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-900 focus:border-transparent"></textarea>
          </div>
        </div>

        <!-- 提交按鈕 -->
        <div class="text-center">
          <button type="submit" :disabled="loading"
            class="bg-blue-900 hover:bg-blue-800 text-white font-bold py-3 px-12 rounded-lg text-lg transition duration-200 disabled:opacity-50 disabled:cursor-not-allowed">
            {{ loading ? '送出中...' : '提交申請' }}
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  age: '',
  education: '',
  birthYear: '',
  birthMonth: '',
  birthDay: '',
  phone: '',
  registeredAddress: '',
  registeredPhone: '',
  registeredHouseOwner: '',
  mailingAddress: '',
  mailingPhone: '',
  mailingHouseOwner: '',
  jobType: '',
  jobDuration: '',
  salary: '',
  hasSalaryTransfer: '',
  hasLaborInsurance: '',
  companyName: '',
  companyAddress: '',
  companyPhone: '',
  hasDriverLicense: '',
  hasGuarantor: '',
  hasSavings: '',
  savingsAmount: '',
  hasCreditCard: '',
  creditNormal: '',
  monthlyCardSpending: '',
  cardPaymentMethod: '',
  loanHistory: '',
  paidInstallments: '',
  paymentNormal: '',
  loanAmount: '',
  loanBankName: '',
  assets: ''
})

const loading = ref(false)
const submitted = ref(false)

const handleSubmit = async () => {
  loading.value = true
  
  try {
    const formData = new FormData()
    
    // 添加所有表單欄位
    Object.keys(form.value).forEach(key => {
      formData.append(key, form.value[key])
    })
    
    // 添加特殊欄位
    formData.append('_captcha', 'false')
    
    const response = await fetch('https://formsubmit.co/ajax/jungkang0911@gmail.com', {
      method: 'POST',
      body: formData
    })
    
    const data = await response.json()
    
    if (data.success === 'true' || response.ok) {
      submitted.value = true
    } else {
      alert('提交失敗，請稍後再試')
    }
  } catch (error) {
    console.error('提交錯誤：', error)
    alert('提交失敗，請稍後再試')
  } finally {
    loading.value = false
  }
}
</script>
