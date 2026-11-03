# 秒懂 AI 伴学 · PC 完整演示

- 当前版本：`20261103-03`（三处页面统一，修正右键菜单SVG图标）。
- 用户目标：在 `changzhi767-byte/xiaowai` 新建独立 `banxue-pc/` 文件夹，补全用户指定 Demo。
- 入口：`dist/banxue-pc/app/index.html#/learning`，或目录根入口。
- 发布状态：GitHub Pages 已发布成功；入口 https://changzhi767-byte.github.io/xiaowai/banxue-pc/ 。仓库独立目录 https://github.com/changzhi767-byte/xiaowai/tree/main/banxue-pc 。

## 本轮对照与补全

源manifest共28条路由，23条有实际页面，5条为`页面待补充`。保留原有试卷、错题、学生学情、学生错题本、学员管理、下载中心及其子页；补齐：

| 模块 | 新增能力 |
| --- | --- |
| 作业批改 | 同源任务列表、筛选/搜索/分页/当天/排序、卡片与表格、审核与材料、上传任务回显、生成实际PDF并进入原下载中心 |
| 语文作文 | 同源作文列表/异常原因/允许重批、审核得分与意见、原新增作文入口、报告下载 |
| 英语作文 | 独立英语任务列表与筛选，沿用英语新增表单，总分约束与异常分支、审核及下载 |
| 学习力诊断 | 同源学员列表、未测评/测评中/已测评、发起确认、第三方承载位、模拟完成/报告/重测/演示PDF |
| 到店 | 学员签到/防重复、在店/离店/全部、日报六态与禁用矩阵、生成/打印/签退/刷新恢复 |

本轮是可操作的静态产品原型，不是真实AI或生产后端；新上传可保存原材料，审核需人工填写，模拟处理用持久化截止时间。诊断沿用已有原型的明确模拟入口，没有自建测评引擎；无扣费、第三方鉴权、家长通知与实体打印机。真实边界在相关页面说明。

## 文件职责与重建

- `source/`：公开参考的原始静态快照。原HTML、模块与资产保留；不可把其5个placeholder误认成最终模块。
- `runtime/common.js`：从原student-detail模块抽取的公共数据、表格/表单/分页、StudentContext、PDF与下载存储；新页面的source为空，工厂base改为正确的`../demos/student-detail/assets/student-data/`。
- `runtime/reference.css`：原student-detail与exam-analysis的真实业务样式。
- `runtime/completion.js/css`：5页的补全实现，不改真实工程或既有错题公开站。
- `build.mjs`：复制基线，新增5个complete-*模块，更新manifest与入口meta/versionHistory；17个原模块字节保留，6个任务模块只安装统一上传adapter并在离页时退出粘贴态。
- `mirror.mjs`：仅用于重新取公开参考；包括catalog动态头像、样本JSON及题图，不只扫描DOM静态引用。重新取基线前先归档当前source，不自动滚动追新。
- `STATE_CONTRACT.md`：逐态合同与恢复/演示边界。
- `verification/`：资源、对照、浏览器与部署证据；不对外发布。

重建：在项目根运行 `node 02-pc版/demos/pc-complete/build.mjs`。

预览：`node 02-pc版/demos/pc-complete/serve.mjs`，打开 `http://127.0.0.1:8765/banxue-pc/app/index.html#/learning`。

该项目使用ES Modules，需HTTP环境，不支持双击file协议。数据仅存在浏览器本地，不上传后端；不同域/浏览器之间不互通。

## 已完成验证

- 1280×720下5个新主模块加载；原学生学情97次/2011题数据与参考一致。
- 作业搜索无结果、重置、状态筛选、表格/卡片切换；待审核改分和意见→报告生成→待下载；生成真实PDF后在原下载中心出现同学员文件。
- 原新增作业→安可→真实选择paper1.png成功→保存→新列表按姓名查到同一任务。
- 诊断启动确认→测评中→明确模拟完成→已测评报告→实际PDF。
- 日报六态按钮矩阵、生成→ready、签到选择排除在店学员、陈一诺签到后6→7人。
- 其余回归与部署证据随最终验收追加；未覆盖真实第三方、生产接口、Windows或实体打印。

## 2026-11-02 发布与最终验收

- 提交 `048767b8d7186347dc97b69f0aeaed5aab386d26`；Actions `41418814372` completed/success，构建、28路由校验、Pages部署各步骤成功。
- 新目录保存README与`source-20261102-01.zip`（17,795,491字节）；SHA256 `b8c3d1dc86f65177cdbb1160b731eeecdcaff0438494ffac76e72b0909e465ef`，本地git blob SHA与GitHub上传结果一致。ZIP中保留发布前源码/文档快照，发布结果以本节及verification/deployment.json为准。
- 由于没有连接器Contents写权限，浏览器所有者登录完成目录创建与源码包上传；Actions以contents:read解压源码到临时目录，执行build与verify，再仅复制运行文件到`banxue-pc/`。没有新建Sites、未改Pages发布源。原workflow先备份，仅增加校验/构建步骤和排除源码ZIP的rsync参数；原coach解包/默认填充步骤逐字保留。
- 原有66个非workflow文件blob SHA全部一致（包括根index、coach-mistake、stage-report与用户创建的`pc端demo`）。14项公开HTTP请求全部200，覆盖旧三个入口、新入口、manifest、5模块、运行脚本、头像和s1数据；证据public-http.json/github-preservation.json。
- 线上逐页确认：中英作文各20任务、诊断161学员、到店6在店学员，均无placeholder、无可见坏图；作业12张首屏卡片正确、meta为20261102-01，console error/warn为空。公开截图github-public.jpg。
- 本地960×720复核页面scrollWidth=viewport=960，二列卡片323px，坏图0；截图chinese-960.jpg。本地新上传任务刷新后变为待审核，审核弹窗显示原paper1.png，未预填虚构分数；取消不修改结果。
- 回归覆盖原六个主模块入口及学情/学员数据、下载记录。原23模块通过字节一致与模块加载检查；没有逐一重跑其全部历史交互，更未声称已验证真实OCR、第三方测评、扣费、家长同步或实体打印。

## 20261102-02 · 错题整理体验版标签

Figma页面9979:13713内真实实例：选中10691:78417、未选中10691:78442。新增49×17px胶囊、9px/13px文字及12px原始sparkle SVG；默认浅蓝#F2F6FF底、#0054FD字，选中透明底/#F2F6FF字及0.5px rgba(242,246,255,.8)内描边。菜单收窄隐藏，展开/peek恢复。仅新增标签，原图标/路由/业务逻辑保留。

实现：build.mjs保留source快照并注入标签，runtime/trial-badge.css及trial-assets为可维护源。根入口/app入口meta及versionHistory同步02。发布构建由原source-20261102-01.zip加trial-20261102-02.zip覆盖后执行build/verify；不能只解压旧源码包就称为最新。trial SHA256=377c4acc6df93cbdc7432b84224e21553a5d1ab078d49516236f69941bbd96bc，workflow副本delivery/publish-pages-trial.yml。

本地默认/选中均49×17，图标naturalWidth=12；两态背景、文字色及内描边computed style正确，收窄display:none、展开恢复，截图与JSON位于verification/trial-*。原28路由及23模块字节一致校验通过；完整包+增量解压重建通过。未发生新的业务踩坑，因此LESSONS未追加。

已发布：提交`2d7b0e0ec26c16dbbcaaea3bf3bb34092f542827`，Actions`41420569881`构建与部署success。线上meta=20261102-02、两态49×17、颜色/描边正确，两份SVG均naturalWidth12；线上证据trial-public.json与trial-selected-public.jpg。原66个非workflow文件SHA一致；本轮仓库README同步了source+trial两段构建关系。

## 20261102-03 · 图片上传组件换为此前定稿版

runtime/image-uploader.js/css为原生上传器适配层，复用此前coach-mistake定稿upload.svg。选择/粘贴/拖入入口500×60、选择按钮104px，灰色hover居中提示，点击再次退出/Esc清焦点，8张整批拒绝，满额禁用但保留入口，删除恢复；下方16px排140px缩略图。原上传器继续拥有文件、排序、全屏预览、缩放、裁剪与回调，未复制Vue内部状态。

覆盖6个任务路由：student/new-task、exam/settings、homework/settings、chinese/new、english/new、wrong-organize/new；考试主卷/答题卡各自8张，作业/作文原PDF入口保留，错题仍仅图片。原文件大小/格式校验、表单字段和提交流程保留。业务源码逆向去掉adapter注入后与基线一致；verify校验28路由、17原样模块和6个仅上传集成差异。

19项原生事件fixture通过：0+9三种入口拒绝、7+2拒绝、7+1成功、8+1拒绝、删除恢复、一次8张、可进可退粘贴、Esc清焦点、拖入前后框/列表几何一致、离页退出保图、140px/16px。真实系统选择avatar-blue.png成功；预览、裁剪取消/应用替换原图、Alt方向键排序通过。6表单7个图片入口均500×60且console无error/warn，原PDF选项数量保留。tests/upload-fixture.mjs生成临时测试页，不进入部署增量包。

最新重建顺序：先解压source-20261102-01.zip，再覆盖trial-20261102-02.zip，再覆盖uploader-20261102-03.zip，执行node build.mjs与node verify.mjs。上传增量含build/verify/adapter/CSS/原SVG/状态契约，避免重新上传完整资源。发布结果待补；无新增踩坑，LESSONS未追加。

发布完成：Actions41422538401 success，提交f68d8df2960d0986744045a68fa53623c0ec2025。uploader ZIP SHA256=b3b1a5da5840739880f0c11b00068f4a1cc12e01660a4a5d1c26dac0ac0c9f95；当前workflow副本delivery/publish-pages-uploader.yml。线上版本03、500×60、原upload.svg地址正常，点击粘贴→Esc退出后activeElement=BODY，console error/warn为空。证据verification/upload-public.json/jpg。原66个非workflow文件SHA一致，仓库README已同步三层归档构建关系。

## 20261102-04 · 按用户截图修正粘贴态

修正上一版保留选择按钮的问题：待粘贴时隐藏104px左入口，“按 ⌘+V 粘贴图片”及退出提示在整个500×60内居中；再次点击/Esc/外点退出后恢复默认选择入口。上传图片、数量限制、预览与裁剪不变。Windows文案按Ctrl+V，未声称实测Windows设备。

22项fixture通过，新增选择按钮隐藏、内部点击区498px全宽、文案含“按”及退出恢复的断言。原有28路由与业务保真校验通过；本次用户纠正已记录L-136并同步项目全局/本地状态契约。参考截图归档verification/paste-reference-04.png。重建在source→trial→uploader三个包之后覆盖paste-20261102-04.zip，再执行build/verify；发布结果见后续记录。

2026-11-03续接发布完成：原修正包和仓库README已在上轮提交，但workflow编辑因自动审批用量上限未执行。本轮补齐发布，提交d9032fcec7f7c1684b50fd2951056a9eae014fb0，Actions41566755315 completed/success。线上meta04，框500×60，内部粘贴点击区498px，中心偏差0；选择按钮display:none，主副文案与截图一致；Esc后入口恢复flex、activeElement=BODY。证据verification/paste-public-04.json/jpg。原66个非workflow文件SHA一致。运行版本沿用已验收04，本轮未再改组件代码，不重复升版。

## 20261103-01 · 对照真实测试环境补全错题整理

真实只读核对与状态矩阵见REAL_ENV_AUDIT.md。新增统一处理态筛选/禁用进度、完成详情知识点与独立解析展开、报告设置两种答案解析模式、本地PDF与原下载中心。原已定稿上传/编辑器保留，错题单张限10MB、8张；首次4个虚构示例标有示例，缺失答案与解析如实为空。source快照不改，runtime/wrong-build.mjs为有前置断言的唯一转换器，wrong-flow.js/css为可维护运行层。

28路由通过；16模块原样，6任务模块仍只安装共享上传adapter，错题列表允许显式业务差异。浏览器已验证样例四态/处理禁用/状态结算、标记筛选与表格同源、详情展开/刷新恢复、报告取消/卷尾选项及实际2页PDF（133479字节）。发布状态待补。新构建在source→trial→uploader→paste之后覆盖wrong-20261103-01.zip。

发布完成：提交030410bd14d7599653846f2211a1f25f1319e4ee，Actions41568829777 completed/success。wrong增量ZIP 26371字节，SHA256=e2f58dc7ce65f8415cfccfd27b6e43cfc859a38dfda0916ab9a8b2f687d811e8；workflow副本delivery/publish-pages-wrong.yml。线上meta=20261103-01，示例四态/处理禁用、知识点/解析、默认无解析的报告设置已验收，坏图0、console error/warn为空。原66个非workflow文件SHA一致。标记提交本地实测1题→后处理→1题完成详情，返回列表保留筛选和表格。证据verification/wrong-public-20261103.jpg及wrong-release-20261103.json。全局状态契约和项目/清单已同步；未发生新增业务踩坑，LESSONS未追加。

## 20261103-02 · 详情抽屉与标记/编辑工作台一起对齐

依据用户本轮要求重新读取真实测试环境DOM/CSS和只读状态，修正上一版只补功能、保留旧编辑器皮肤的不足。状态矩阵见VISUAL_STATE_MATRIX.md。详情640px/32%遮罩、头86px/尾56.5px、单列608px题卡、题图和解析同白框、解析14px+箭头、展开隐藏外知识点并保留空间；报告设置实际340×228，默认卷尾解析（本项覆盖01版默认无解析的推断）。

标记及编辑全屏56px顶栏，左160.5px导航、标记右250px题卡/32px标题、编辑隐藏右栏但保留左导航；真实缩放图标、红色笔迹及控件分层。补齐之前漏镜像的笔迹素材，提交裁图也绘制同一笔迹，详情/PDF可回显。编辑默认蓝虚线/浅蓝底、选中蓝2px/四角圆点及四边缩放区；姓名旁双列12年级/9学科菜单，立即预览但归属编辑事务；右键合并/拆开/删除，禁用项保留。原坐标/拖动/缩放/归属/撤销及快照存储复用；本轮未另建手势算法。

已浏览器验证：抽屉实际几何、单列/展开、红笔资产和裁图回显、真实paper1.png选择→下一步→前处理→标记；年级学科修改后返回回滚、确认后刷新恢复高二/物理；批量合并/拆开禁用矩阵、删除/撤销、清空取消/确认/撤销；960px编辑页scrollWidth=960，左导航保留、右栏隐藏、纸张未溢出。原几何手势实现保持，本轮未重跑全部历史鼠标拖动/缩放边界组合。28路由/16原模块保真通过；4任务模块仅上传适配，2个带错题编辑器的模块与错题列表允许显式集成差异。

两个现有公开题图样例经人工校对补B/13根和相应演示解析，只按示例题图名称启用；用户新上传不预填答案，不调用真实OCR或答案服务。知识点与学员仍为原演示数据。LESSONS追加L-137。发布待补；最新源码在source→trial→uploader→paste→wrong之后覆盖visual-20261103-02.zip。

发布完成：提交dbdc255e8f31aad66a159ddcc71b21ba9d8025ed，Actions41572146532 completed/success。visual增量包41832字节，SHA256=dbc664d8a4c22f5f7ab90af76c7ddb4469a0f1939373b9cbd33f3a3c77cd60e2，workflow副本delivery/publish-pages-visual.yml。线上meta02、抽屉640/头86/尾56.5/卡608、报告340×228默认tail、编辑左160.5/右栏隐藏/选中2px蓝边/笔迹资源正常；缓存返回重入仍workbench/hidden，坏图0、console error/warn为空。原66个非workflow文件SHA一致。新版含示例解析PDF实际下载197424字节、2页、%PDF-1.4。截图/JSON见verification/*-public-20261103-02.*；上传→下一步→编辑/标记及960px证据为*-local-20261103-02.jpg和状态矩阵记录。原始归档为发布前源码快照，最终状态以本README及Actions为准。

## 20261103-03 · 最终截图复核修正菜单图标

02线上候选截图发现右键菜单伪元素默认mask规则优先级更高，合并/拆开/删除画成实色色块。提高专用SVG规则优先级后，三项mask-image均为真实环境SVG且截图正确，禁用矩阵不变；28路由通过。未更改02已验收的抽屉/字段事务/标记/裁图/PDF及上传。最新完整视觉增量visual-20261103-03.zip替代visual-20261103-02.zip，不继续叠加；重建顺序source→trial→uploader→paste→wrong→visual03。源码及本README由既有工作流部署，最终结果见仓库Actions；02历史记录保留。
