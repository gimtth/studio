<template>
  <section id="recruitment" class="recruitment">
    <div class="container">
      <div class="section-title">
        <h2>招新专栏</h2>
        <p>加入我们，参与技术培训、校园信息化项目与赛事，一起成长！</p>
      </div>
      <div class="recruitment-content">
        <div class="recruitment-text">
          <h3>2025年招新正式启动</h3>
          <p>热爱网络技术、运维、安全或新媒体创意？无论有无基础，都欢迎加入，与我们一起服务校园、精进技能。</p>
          <div class="recruitment-requirements">
            <h4>招新要求</h4>
            <ul class="requirements-list">
              <li>郑州升达经贸管理学院在校学生，态度端正、责任心强；</li>
              <li>对网络技术、编程、运维等方向有浓厚兴趣（有无基础均可）；</li>
              <li>愿意投入时间参与学习和工作，服从工作室安排；</li>
              <li>有团队协作精神，乐于分享和帮助他人。</li>
            </ul>
          </div>
          <h4>招新流程与时间</h4>
          <p>电子简历：关注“升达网络技术工作室”公众号，点击“招新快看”获取/提交。</p>
          <p>纸质简历：资讯楼319领取与投递；招新时间 9月5日-9月30日 周一至周五 16:30-20:30。</p>
          <p>流程：在线报名/纸质投递 → 初审 → 面试 → 录用培训。</p>
        </div>
        <div class="recruitment-form">
          <h3 class="form-title">在线报名</h3>
          <form @submit.prevent="submitForm">
            <div class="form-group" v-for="field in fields" :key="field.id">
              <label :for="field.id">{{ field.label }}</label>
              <select
                v-if="field.type === 'select'"
                class="form-control"
                :id="field.id"
                v-model="form[field.id]"
                required
              >
                <option value="">请选择意向部门</option>
                <option value="业务部">业务部</option>
                <option value="技术部">技术部</option>
                <option value="网安小组">网安小组</option>
                <option value="运维小组">运维小组</option>
                <option value="新媒体小组">新媒体小组</option>
              </select>
              <textarea
                v-else-if="field.type === 'textarea'"
                class="form-control"
                :id="field.id"
                v-model="form[field.id]"
                :placeholder="field.placeholder"
                :required="field.required"
              ></textarea>
              <input
                v-else
                class="form-control"
                :id="field.id"
                v-model="form[field.id]"
                :placeholder="field.placeholder"
                :required="field.required"
                :type="field.inputType || 'text'"
              />
            </div>
            <button type="submit" class="btn full-btn">提交报名</button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { reactive } from 'vue'

type FormState = {
  name: string
  studentId: string
  college: string
  department: string
  phone: string
  intro: string
}

type Field =
  | { id: keyof FormState; label: string; placeholder: string; required: boolean; type?: 'textarea'; inputType?: string }
  | { id: keyof FormState; label: string; placeholder: string; required: boolean; type: 'select'; inputType?: string }

const form = reactive<FormState>({
  name: '',
  studentId: '',
  college: '',
  department: '',
  phone: '',
  intro: '',
})

const fields: Field[] = [
  { id: 'name', label: '姓名', placeholder: '请输入你的姓名', required: true },
  { id: 'studentId', label: '学号', placeholder: '请输入你的学号', required: true },
  { id: 'college', label: '学院', placeholder: '请输入你的学院', required: true },
  { id: 'department', label: '意向部门', placeholder: '', required: true, type: 'select' },
  { id: 'phone', label: '联系电话', placeholder: '请输入你的手机号', required: true, inputType: 'tel' },
  { id: 'intro', label: '个人简介/技能特长', placeholder: '请简要介绍自己，可说明相关技能或兴趣方向', required: false, type: 'textarea' },
]

const submitForm = () => {
  alert('报名提交成功！我们将尽快与你联系，请保持电话畅通～')
  form.name = ''
  form.studentId = ''
  form.college = ''
  form.department = ''
  form.phone = ''
  form.intro = ''
}
</script>

<style scoped>
.recruitment {
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(241, 240, 255, 0.82));
  position: relative;
  overflow: hidden;
}

.recruitment::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 18% 18%, rgba(255, 111, 97, 0.16), transparent 32%),
    radial-gradient(circle at 82% 12%, rgba(124, 58, 237, 0.16), transparent 30%);
  pointer-events: none;
}

.recruitment-content {
  position: relative;
  z-index: 1;
  display: flex;
  flex-wrap: wrap;
  gap: 50px;
  align-items: center;
}

.recruitment-text {
  flex: 1;
  min-width: 300px;
}

.recruitment-text h3 {
  font-size: 28px;
  color: var(--color-primary);
  margin-bottom: 20px;
  font-family: var(--font-display);
}

.recruitment-text p {
  font-size: 16px;
  color: var(--color-muted);
  margin-bottom: 20px;
  line-height: 1.8;
}

.recruitment-requirements h4 {
  font-size: 20px;
  margin-bottom: 15px;
  color: var(--color-secondary);
  letter-spacing: 0.3px;
}

.requirements-list {
  list-style: none;
  margin-bottom: 30px;
}

.requirements-list li {
  font-size: 16px;
  color: var(--color-text);
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.requirements-list li::before {
  content: '✓';
  color: var(--color-primary);
  margin-right: 10px;
  font-weight: bold;
}

.recruitment-form {
  flex: 1;
  min-width: 300px;
  background: linear-gradient(150deg, rgba(255, 255, 255, 0.9), rgba(245, 233, 255, 0.82));
  padding: 30px;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  border: 1px solid rgba(255, 255, 255, 0.6);
}

.form-title {
  text-align: center;
  margin-bottom: 20px;
  color: var(--color-secondary);
  font-family: var(--font-display);
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-size: 14px;
  color: var(--color-text);
  font-weight: 600;
}

.form-control {
  width: 100%;
  padding: 12px;
  border: 1px solid rgba(255, 255, 255, 0.7);
  border-radius: var(--radius-md);
  font-size: 14px;
  transition: border-color 0.3s, box-shadow 0.3s;
  background: rgba(255, 255, 255, 0.8);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.6);
}

.form-control:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 4px rgba(255, 111, 97, 0.2);
}

textarea.form-control {
  min-height: 100px;
  resize: vertical;
}

.full-btn {
  width: 100%;
}
</style>
