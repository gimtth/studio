<template>
  <section id="services" class="services">
    <div class="container">
      <div class="section-title">
        <h2>服务中心</h2>
        <p>内修、外修、星印云自助打印机维修三大业务，覆盖校园网与设备全场景。</p>
      </div>
      <div class="services-list">
        <div
          class="service-card"
          v-for="service in services"
          :key="service.id"
          :class="{ active: activeService === service.id }"
          @click="selectService(service.id)"
        >
          <div class="service-icon">
            <i :class="service.icon"></i>
          </div>
          <h3>{{ service.title }}</h3>
          <p>{{ service.desc }}</p>
        </div>
      </div>

      <div class="services-detail" v-if="currentService">
        <div class="detail-header">
          <div class="detail-title">
            <span class="pill">{{ currentService.title }}</span>
            <h4>{{ currentService.title }} · 服务详情</h4>
            <p class="detail-desc">{{ currentService.detail }}</p>
          </div>
        </div>

        <div v-if="currentService.id === 'inner'" class="detail-body">
          <div class="software-search">
            <input
              v-model="softwareKeyword"
              type="text"
              placeholder="搜索可免费安装的软件名称或类别…"
            />
            <span class="count">共 {{ filteredSoftware.length }} 条</span>
          </div>
          <div class="software-list">
            <div
              v-for="item in filteredSoftware"
              :key="item.text + item.type"
              class="software-item"
              :class="{ group: item.type === 'group' }"
            >
              {{ item.text }}
            </div>
          </div>
        </div>

        <div v-else class="detail-body">
          <ul class="detail-points">
            <li v-for="point in currentService.points" :key="point">{{ point }}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

type ServiceId = 'inner' | 'outer' | 'printer'

const services: Array<{
  id: ServiceId
  icon: string
  title: string
  desc: string
  detail: string
  points?: string[]
}> = [
  {
    id: 'inner',
    icon: 'fas fa-wifi',
    title: '内修服务',
    desc: '免费电脑系统、软件安装，处理校园网账号相关问题、IP绑定与基础网络配置。',
    detail: '电脑系统安装、常用软件免费部署，账号/IP 设置指导，宿舍/办公网络基础配置支持。',
  },
  {
    id: 'outer',
    icon: 'fas fa-laptop-code',
    title: '外修服务',
    desc: '宿舍网络故障排查、网线修复、上门支持与安全咨询。',
    detail: '网络连通性检查、网线制作/修复、校园网异常诊断、入户排查与安全使用建议。',
    points: ['宿舍网络掉线/限速排查', '网线制作与接口修复', '校园网账号异常快速处理', '提供安全使用指引'],
  },
  { 
    id: 'printer',
    icon: 'fas fa-project-diagram', 
    title: '星印云打印机',
    desc: '自助打印机维护、耗材支持与故障处理。',
    detail: '星印云自助打印机巡检维护，异常故障定位与恢复，耗材更换。',
    points: ['打印异常处理与重置', '耗材更换与日常巡检','故障处理'],
  },
]

const activeService = ref<ServiceId>('inner')
const softwareKeyword = ref('')

const softwareCatalog = [
  '*压缩解压',
  '360压缩',
  'WinRAR',
  'Bandizip',
  '7-Zip & HaoZip',
  '*游戏工具',
  'Steam下载管家',
  '迅雷网游加速器',
  'Golink网游加速器',
  '雷神网游加速器',
  '*浏览器',
  '谷歌 & Edge浏览器',
  '360 & QQ浏览器',
  '火狐浏览器',
  '搜狗浏览器',
  '*即时通讯',
  '腾讯会议',
  '微信（官方+多开版）',
  '企业微信',
  '钉钉  & 千牛',
  'QQ ‍&‍  腾讯TM',
  'QT语音  & YY语音',
  '*输入法',
  '百度 & 迅雷官方版',
  '百度 & 讯飞输入法',
  '极品输入法',
  'Rime输入法',
  '*下载工具',
  '百度 & 迅雷官方版',
  '比特彗星 & Motrix',
  '闪豆视频下载器',
  '硕鼠下载器',
  'qBittorrent',
  'Free Download Manager',
  '*媒体播放',
  'QQ & 酷狗（官方版）',
  '网易云（官方版）',
  '网易云（官方版）	Listen1',
  'QQ影音 & 完美解码',
  'РotРlayer & QuickTime',
  '*杀毒软件',
  '360 & 火绒安全卫士',
  '腾讯电脑管家',
  '金山毒霸',
  '小红伞',
  '*系统优化',
  'Wise Care 365',
  'Glary Utilities',
  'Advanced SystemCare',
  'Ashampoo WinOptimizer',
  'zTasker',
  'R-Wipe & Clean',
  '*系统维护',
  '傲梅分区助手',
  'dll修复工具',
  '软媒蓝屏助手',
  '.net修复工具',
  '微软运行库',
  '图吧工具箱',
  '*驱动修复',
  '驱动人生（含离线版）',
  '驱动总裁离线版',
  '360驱动大师（含离线版）',
  '驱动精灵（含离线版）',
  '*卸载工具',
  'IObitUninstaller',
  'Uninstall Tool',
  'Geek Uninstaller',
  'Wise Force Deletet',
  '*主题壁纸',
  'WinDynamicDesktop',
  'Lively Wallpaper',
  'AutoDarkModeX',
  '360桌面助手',
  '*截图软件',
  'Snipaste',
  'PixPin',
  'Screen to Gif',
  'FastStone Capture',
  '*录屏软件',
  '班迪录屏',
  '360录屏',
  'Movavi Screen Recorder',
  'Icecream Screen Recorder',
  '屏幕录像专家',
  'Mirillis Action',
  'oCam',
  'EVCapture',
  '*远程控制',
  'ToDesk & RustDesk',
  '向日葵',
  'AnyViewer',
  'RayLink',
  '*效率工具',
  'XYplorer',
  'Everything',
  'Stardock Fences',
  'OneCommander',
  '❖操作系统',
  '*常用工具',
  '微PE工具箱',
  'VMware',
  '*操作系统',
  'Windows11',
  'Windows10',
  'Windows7',
  'CentOS Linux',
  'Ubun Linux',
  'openLylin',
  'Deepin',
  '统信UOS',
  '*安卓模拟器',
  '雷电模拟器',
  '蓝叠模拟器',
  '❖办公软件',
  'Office',
  'WPS',
  'Project',
  'Visio',
  'Xmind',
  'EdrawMax',
  'OfficeSuite',
  'Typora',
  'Draw.io',
  'SimpleMind',
  'Freeplane',
  'Sketchpad（几何画板）',
  '手写模拟器',
  'OCR文字识别',
  'LocalSend',
  'Escrcpy',
  'VueScan',
  'ToDoList',
  '❖PDF编辑',
  'Acrobat DC',
  'Solid Converter PDF',
  'PDF Candy	PDFgear',
  'PDF-XChange',
  'PDF24 Creator',
  'PDF Shape	PDFelement',
  'Master PDF Editor	UPDF',
  '❖文献工具',
  'EndNote',
  'CAJView',
  'NoteExpress',
  'LaTex',
  'Zotero',
  '论文潜搜',
  'CiteSpace',
  'Mendeley',
  '❖翻译软件',
  'DeepL',
  'TranSmart',
  'STranslate',
  'pot',
  'CopyTranslator',
  '知云文献翻译',
  '❖AI-工具',
  'DeepSeek',
  'Stable Diffusion',
  'OfficeAI',
  '即创AI & Kimi AI',
  'Apt Full',
  '讯飞星火',
  'AI FaceSwap',
  '百度AI图片创作助手',
  '❖图像处理',
  'Photoshop（PS）',
  'PS插件库',
  'Lightroom（LrC）',
  'illustrator（Ai）',
  'PS Elements（PS简化版）',
  'Nik Collection',
  'InDesign（Id）',
  'InCopy（Ic）',
  'ACDSee',
  '光影魔术手',
  'QuarkXPress',
  'Clip Studio Paint',
  'DxO PhotoLab',
  'DxO FilmPack',
  'DxO PureRAW',
  'DxO ViewPoint',
  'Topaz Gigapixel Ai',
  'Topaz Photo Ai',
  'Topaz DeNoise Al',
  'Aiarty Image',
  'Capture One',
  'SketchBook',
  'Bridge（Br）',
  'Corel Painter',
  'PaintTool SAI',
  'Krita',
  '❖媒体动画',
  '*视频编辑',
  'Premier（Pr）',
  'Pr插件库',
  'After Effects（Ae）',
  'Ae插件库',
  'Edius',
  '威力导演',
  'Media Encode（Me）	 Topaz Video AI',
  'Prelude',
  'Pr Element（Pr简化版）',
  'Freemake Video Converter	格式工厂',
  '快剪辑	剪映 &‍ CapCut',
  '*音频编辑',
  'Audition（Au）',
  'Cubase',
  'Nuendo',
  'Ableton Live',
  'Audacity	Mixxx',
  '*动画制作',
  'Maya',
  'Cinema 4D（C4D）',
  'Octane for C4D',
  'Arnold（阿诺德）for C4D',
  'Corona for C4D',
  'Character Animator（Ch）',
  '❖AutoCAD',
  '*CAD软件',
  'CAD',
  'CAD精简版',
  'CAD机械版',
  'CAD建筑版',
  'CAD电气版',
  'CAD MEP',
  'CAD Plant 3D',
  'CAD Map 3D',
  '*国产CAD',
  '中望CAD',
  '中望CAD建筑版',
  '中望CAD机械版',
  '浩辰CAD',
  '*CAD工具',
  '天正软件',
  'CAD插件库',
  'CAXA电子图板',
  'CAXA工艺图表',
  'CAXA3D实体设计',
  'CAXA CAM',
  '❖3D 设计',
  '3ds Max',
  'V-ray for 3ds Max',
  'Corona for 3ds Max',
  'Arnold（阿诺德）for 3ds Max',
  'Lumion	Live2D',
  'SketchUp（草图大师）',
  'Enscape',
  'V-Ray for SketchUp',
  '坯子库 for SketchUp',
  'Marmoset Toolbag（八猴）',
  'Substance 3D Designer',
  'Substance 3D Painter',
  'Substance 3D Sampler',
  'Zbrush',
  'Blender',
  'ArchiCAD',
  'KeyShot',
  'CorelCAD',
  'Dimension（Dn）',
  'Artlantis',
  'Modo',
  'SideFX Houdini FX	SimLab Compose',
  'Cascadeur',
  '酷家乐',
  '❖机械设计',
  'SolidWorks（SW）',
  'Mastercam',
  'Rhinoceros（犀牛）',
  'V-ray for Rhino',
  'Pro/E',
  'Creo',
  'UG NX',
  'CATIA',
  'CATIA Composer',
  'PowerMill',
  'Inventor',
  'Solid Edge',
  'AlphaCAM',
  'PixyzStudio',
  'WorkNC',
  'GibbsCAM',
  '❖建筑设计',
  'Revit（BIM）',
  'Navisworks',
  'Civil 3D',
  'Fuzor',
  'Tekla Structures',
  'Vectorworks',
  '❖网页设计',
  'Dreamweaver（DW）',
  'Axure',
  'Animate（An）',
  'Flash',
  'Adobe XD',
  'Fireworks',
  '❖开发编程',
  'Visual Basic（VB）',
  'Visual C++（VC）',
  'Dev C++',
  'Java',
  'HBuilder X',
  'PSPAD editor',
  'Sublime Text',
  'Notepad++',
  'DBeaver Ultimate',
  'R语言 & RStudio',
  'Anaconda',
  'Android Studio',
  'MyEclipse',
  'eclipse',
  'Visual Studio',
  'Visual Studio Code',
  'Labview',
  'Python',
  'Unity 3D',
  'Keil uVision',
  'IntelliJ IDEA',
  'PhpStorm',
  'WebStorm',
  'PyCharm',
  'RubyMine',
  'goland',
  'Rider',
  'CLion',
  'DataGrip',
  'Quartus II',
  'CIMCO Edit',
  'Step7',
  '❖理科工具',
  'Matlab',
  'Origin',
  'Mathematica',
  'Tableau',
  'SAS',
  'Amos',
  'AxMath',
  'Mplus',
  'Minitab',
  'Lingo',
  'MathCAD',
  'FX Draw Tools',
  'Design Exper',
  'Maple',
  'Cytoscape',
  'EViews',
  'NCSS',
  'SQL Server',
  'MySQL',
  'Navicat Premium',
  'SigmaPlot',
  'Avantage',
  '❖仿真模拟',
  'ANSYS',
  'ANSYS Electronics',
  'ANSYS Lumerical',
  'ANSYS EMA3D',
  'Abaqus',
  'Moldflow',
  'Adams',
  'Tecplot 360 EX',
  'Tecplot Focus',
  'Tecplot RS',
  'midas Civil',
  'midas NFX',
  'midas Gen',
  'FLAC3D',
  'DEFORM',
  'Dynaform',
  'Altair Hyperwork',
  'Altair EDEM',
  'PLAXIS2D	PLAXIS3D',
  'Ansoft Maxwell',
  'JMatPro',
  'VERICUT',
  'Materials Studio',
  '❖电子电路',
  'Altium Designer（AD）',
  'MotorSolve',
  'Multisim',
  'Proteus',
  'Cadence SPB	Altair PSIM',
  'Advanced Design System',
  '❖行业软件',
  'EPLAN Electric',
  'TIA Portal （博途）',
  'Win CC',
  'GX Works',
  'ENVI',
  'hyperMILL',
  'Oligo	Marvelous Designer',
  'Ansys Zemax OpticStudio',
  'MDI Jade',
  'ArcGIS	PCL Geomatica',
  'Autodesk Mudbox',
  'Autodesk Vred',
  'Alias AutoStudio',
  'Autodesk ArtCAM',
  'PASS',
  'Global Mapper',
  'ABB RobotStudio',
  'jewelCAD',
  'Vero Visi	Google Earth',
  'MedCalc',
  'Kisssoft',
  'LabSpec',
  'Gaussian',
  'Materialise Mimic',
].filter((line) => line && line.trim().length > 0)

const softwareEntries = softwareCatalog.map((line) => {
  const trimmed = line.trim()
  const isGroup = trimmed.startsWith('*') || trimmed.startsWith('❖')
  const text = trimmed.replace(/^[*❖]\s*/, '')
  return { text, type: isGroup ? 'group' : 'item' as const }
})

const currentService = computed(() => services.find((s) => s.id === activeService.value))

const filteredSoftware = computed(() => {
  const keyword = softwareKeyword.value.trim().toLowerCase()
  if (!keyword) return softwareEntries
  return softwareEntries.filter((entry) => entry.text.toLowerCase().includes(keyword))
})

const selectService = (id: 'inner' | 'outer' | 'printer') => {
  activeService.value = id
}
</script>

<style scoped>
.services-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

.service-card {
  background: #fff;
  border: 1px solid rgba(0, 0, 0, 0.05);
  padding: 24px 20px;
  border-radius: 12px;
  text-align: center;
  transition: all 0.2s ease;
  box-shadow: var(--shadow-card);
  position: relative;
  overflow: hidden;
}

.service-card h3 {
  font-size: 20px;
  margin-bottom: 15px;
  color: var(--color-text);
  font-weight: 700;
}

.service-card:hover {
  transform: translateY(-8px) scale(1.01);
  box-shadow: var(--shadow-soft);
}

.service-card::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(79, 139, 255, 0.16), rgba(255, 122, 214, 0.12));
  opacity: 0;
  transition: opacity 0.2s ease;
  pointer-events: none;
}

.service-card:hover::after,
.service-card.active::after {
  opacity: 1;
}

.service-card p {
  font-size: 14px;
  color: var(--color-muted);
}

.service-card.active {
  border-color: rgba(79, 139, 255, 0.4);
  box-shadow: 0 14px 32px rgba(79, 139, 255, 0.15);
}

.services-detail {
  margin-top: 24px;
  background: rgba(255, 255, 255, 0.92);
  border: 1px solid rgba(255, 255, 255, 0.6);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  padding: 20px;
}

.detail-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  border-bottom: 1px dashed rgba(0, 0, 0, 0.08);
  padding-bottom: 12px;
  margin-bottom: 16px;
}

.detail-title h4 {
  margin: 6px 0 4px;
  font-size: 18px;
  color: var(--color-text);
}

.detail-desc {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.6;
}

.pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 10px;
  background: rgba(79, 139, 255, 0.12);
  color: var(--color-primary);
  border-radius: 999px;
  font-size: 12px;
  font-weight: 600;
}

.detail-body {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.detail-points {
  margin: 0;
  padding-left: 18px;
  color: var(--color-muted);
  line-height: 1.6;
}

.software-search {
  display: flex;
  align-items: center;
  gap: 10px;
}

.software-search input {
  flex: 1;
  padding: 10px 12px;
  border-radius: 10px;
  border: 1px solid rgba(0, 0, 0, 0.08);
  background: rgba(255, 255, 255, 0.9);
}

.software-search .count {
  font-size: 13px;
  color: var(--color-muted);
}

.software-list {
  max-height: 320px;
  overflow: auto;
  border: 1px solid rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  padding: 12px;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.95), rgba(248, 250, 255, 0.9));
  display: grid;
  gap: 6px;
}

.software-item {
  padding: 6px 10px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.8);
  color: var(--color-muted);
  font-size: 14px;
  line-height: 1.4;
}

.software-item.group {
  background: rgba(79, 139, 255, 0.12);
  color: var(--color-primary);
  font-weight: 700;
}

@media (max-width: 992px) {
  .services-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .services-list {
    grid-template-columns: 1fr;
  }
}
</style>
