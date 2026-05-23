# AI 代理名冊 — 分類拆分版

> 蒸餾自 [`ai_agent_video_production_workflow.md`](./ai_agent_video_production_workflow.md)。
> 每張表格新增兩個 **推導欄位** — *工具存取* 與 *架構模式* — 由代理的職責推導出來，並對照 2026 年業界工具與已發表的 AI 代理研究。

---

## 目錄

1. [前線製作代理 (1–5)](#1-前線製作代理)
2. [攝影與燈光代理 (6–8)](#2-攝影與燈光代理)
3. [剪接與調色代理 (9–18)](#3-剪接與調色代理)
4. [聲音與音樂代理 (19–22)](#4-聲音與音樂代理)
5. [表演與編舞代理 (23–27)](#5-表演與編舞代理)
6. [發行與市場推廣代理 (28–31)](#6-發行與市場推廣代理)
7. [教育與領域專家代理 (32–45)](#7-教育與領域專家代理)
8. [AI 紀元專業代理 (46–52)](#8-ai-紀元專業代理)
9. [特殊元代理 (53–80)](#9-特殊元代理)
10. [AI 代理共同架構](#10-ai-代理共同架構)
    - [10.1 架構示意圖](#101-架構示意圖)
    - [10.2 元件參考表](#102-元件參考表)
11. [參考資料](#11-參考資料)

---


## 1. 前線製作代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | **DirectorAgent** | 掌握創意願景；發出鏡頭意圖、設定節奏、核准鏡次 | Criterion 評論音軌；IMDb 前 250 名導演訪談；DGA 研討會；MasterClass（Scorsese/Lynch/Gerwig） | 鏡頭意圖忠實度（CLIP-T ≥0.32）；故事節拍覆蓋率 100%；節奏曲線符合類型先驗 | 在盲測成對比較中對 DGA 剪接版勝率 ≥55%（Arena） | ScreenwriterAgent、EditorAgent、AudienceSim — JSON 評論匯流排 | EditorAgent、DoPAgent、ScreenwriterAgent、ComposerAgent | Sora 2 API、Veo 3.1 (Gemini API)、Runway Gen-4、Kling 3.0；DaVinci Resolve（經由 MCP） | Self-Refine + LLM-as-Judge（評分準則：類型先驗） |
| 2 | **ProducerAgent / EP** | 預算、排程、招聘、交付；審批階段關卡 | PGA Producers Mark；Variety/Deadline 預算洩露；LineProducer Excel 語料 | 準時交付率；預算偏差 <±5%；人才滿意度（RLHF） | 以 0.6× 成本擊敗 PGA 排程且 CSAT 相同 | 所有下游代理（升級）；最終綠燈由 HiTL 關卡 | DirectorAgent（範圍蔓延）、所有代理（資源消耗） | Google Sheets API、Airtable、Temporal/Airflow 編排、Stripe 計費 | 代理圖（LangGraph DAG）+ ReAct 工具呼叫 |
| 3 | **ScreenwriterAgent** | 處理方案 → 劇本；對白；結構 | Black List 劇本；WGA 圖書館；McKee《Story》；Truby；Kaufman/Sorkin 訪談 | Save-the-Cat 節拍通過；對白獨特性（嵌入距離 ≥τ）；改寫差異 | 在盲測閱讀對 Black List 前 10 名勝率 ≥50%（模擬 WGA 評判） | DirectorAgent、DramaturgAgent、StoryEditorAgent — Reflexion 循環 | DirectorAgent（大綱清晰度）、DialogueAgent、ConsistencyAgent | Fountain/FDX 格式驗證器；語意嵌入模型（text-embedding-3-large） | Reflexion (Shinn 2023) — 帶情節記憶的口頭強化學習 |
| 4 | **ShowrunnerAgent** | 跨集故事弧、編劇室編排 | WGA 節目總監培訓；Sopranos/BB 編劇室記錄；Mike Schur 教材 | 弧線連續性得分；角色線索完成度；調性變異在範圍內 | 10 集內系列聖經覆蓋率 ≥99%（人類基準 ~95%） | NetworkNotes 代理、AudienceSim、與 ScreenwriterAgent 多代理辯論 | ScreenwriterAgent（故事弧）、CastingAgent、DirectorAgent（單集調性） | 長上下文 LLM（Gemini 2.5 Pro 1M）、向量資料庫（Pinecone/Weaviate）做聖經搜尋 | 多代理辯論 (Du 2023) + MemoryAgent 檢索 |
| 5 | **CastingAgent** | 語音及肖像選角；試鏡模擬 | CSA Artios 檔案；SAG-AFTRA AI 附加條款；已同意配音演員語料 | 角色聲音匹配度（觀眾偏好）；同意合規 100% | 在盲測偏好中擊敗 CSA 選角；數小時 vs 數週 | DirectorAgent、ShowrunnerAgent、Legal/ConsentAgent | VoiceCloneAgent（肖像）、AvatarDesignAgent | ElevenLabs v3 聲音庫、HeyGen 虛擬主播目錄、speaker-embedding 相似度（Resemblyzer） | LLM-as-Judge（聲音樣本成對偏好） |


---

## 2. 攝影與燈光代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 6 | **CinematographerAgent (DoP)** | 鏡頭、燈光、構圖、視覺風格 | ASC Magazine 1980–至今；Deakins 論壇；Brown《Cinematography: Theory & Practice》；康城入選鏡頭庫 | 三分法／引導線得分；曝光直方圖在區域內；色溫一致性 | 在美學盲測偏好中擊敗 ASC 同行評審短片 | DirectorAgent、ColoristAgent、VFXSupAgent | DirectorAgent（視覺意圖）、GafferAgent、ColoristAgent | Veo 3.1（鏡頭路徑控制）、Runway Gen-4（ControlNet 引導）、ACES 調色管線工具 | Self-Refine + 基於 CLIP 的美學評分 |
| 7 | **CameraOperatorAgent** | 按 DoP 意圖執行構圖／對焦／移動 | SOC 檔案；Steadicam 工作坊精華；現場跟焦遙測 | 畫面穩定性、對焦命中率、動作置中 | 對焦準確度 >99%（SOC 基準 ~97%） | CinematographerAgent（鏡次回饋） | CinematographerAgent（不切實際的要求） | Runway 鏡頭路徑預設；Kling 動態控制 API；虛擬攝影機機架（Unreal MV） | ReAct (Yao 2022) — 推理構圖後呼叫渲染器 |
| 8 | **DronePilotAgent** | 空中攝影（模擬或真實） | Philip Bloom 教學；FAA Part 107；SkyPixel 獲獎精華 | 路徑平滑度；地理圍欄合規 100%；地平線穩定性 | 以 10× 出勤率達比賽級平滑度；零空域違規 | DoPAgent、SafetyAgent | DoPAgent（不可能高度）、SafetyAgent（風險） | DJI Waypoint SDK（模擬）；Veo 3.1 空拍模式；地理圍欄資料庫（AirMap API） | 憲法式 AI（安全憲法：FAA 規則作為原則） |




---

## 3. 剪接與調色代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 9 | **EditorAgent** | 組合剪接；節奏；鏡頭覆蓋選擇 | Murch《In the Blink of an Eye》；ACE Eddie 獲獎作品；Sundance 剪接實驗室 | 節奏曲線符合類型；Murch「六法則」分數；AVD ≥ 目標 | 對 ACE 認證剪接版成對勝率 ≥55% | DirectorAgent、AudienceSim、ComposerAgent（音樂剪接同步） | DirectorAgent（覆蓋過多）、DoPAgent（無法使用的鏡次） | DaVinci Resolve（經由 MCP 橋接）；FFmpeg；EDL/XML 時間軸 API | Self-Refine（評分準則：Murch 六法則） |
| 10 | **ColoristAgent** | 最終調色；風格一致性 | ICA 課程；Sonnenfeld 調色實錄；HPA 獲獎調色 | ΔE 漂移 <2；膚色 IT8 對齊；情緒向量匹配 | 在盲測偏好中擊敗初級調色師；於 ΔE 預算內匹配資深 | DoPAgent、DirectorAgent、AccessibilityAgent（對比度） | DoPAgent（混合色溫）、VFXAgent（合成色彩不匹配） | DaVinci Resolve 色彩 API（MCP）；ACES/OCIO 管線；LUT 生成器 | Self-Refine + 工具使用（色度計驗證） |
| 11 | **VFXSupervisorAgent** | 規劃與監督 VFX 管線 | VES 獎項；SIGGRAPH 論文；Weta/DNEG 公開演講；Foundry 培訓 | 鏡頭完成率；合成像素誤差；CLIP-T vs 母片 | 達到 Weta 級 QC 通過率而耗時減少 | DirectorAgent、DoPAgent、ConsistencyAgent | AIGeneratorAgent（瑕疵）、CompositorAgent | Nuke（經由 MCP 橋接）；Runway Gen-4 Aleph（影片轉影片）；ComfyUI | 代理圖（每鏡頭並行扇出）+ LLM-as-Judge（QC 評分） |
| 12 | **AnimatorAgent (2D/3D)** | 角色動作、重量、節奏 | Williams《Animator's Survival Kit》；Annie 獎；Pixar SparkShorts；Aaron Blaise 課程 | 12 法則檢查清單分數；弧線平滑度；嘴形對音準確度 | 在 Annie 評分準則上擊敗初級動畫師；以 5× 產能匹配資深 | DirectorAgent、LipSyncAgent | StoryboardAgent（不可能動作）、DirectorAgent（節奏意見） | Kling 3.0 動態控制；Blender Python API；Cascadeur 物理；Sync.so 嘴形 | Self-Refine（評分準則：12 法則檢查表） |
| 13 | **MotionGraphicsAgent** | 動態文字、下三分之一、資訊圖 | Motionographer 檔案；School of Motion 課程；AICP Next 獲獎 | 字體層次得分；品牌系統合規；縮圖大小可讀性 | 在速度 + 符合品牌的代理 RFP 比拼中勝出 | BrandManagerAgent、AccessibilityAgent（對比度） | CopywriterAgent（贅言）、EditorAgent（時序） | After Effects（經由 MCP/ExtendScript）；Lottie 匯出；Rive；品牌資產 CDN | ReAct — 對品牌指引推理後渲染 |
| 14 | **StoryboardAgent** | 劇本 → 鏡頭分鏡 | Mateu-Mestre《Framed Ink》；Pixar story-trust 輸出；Sylvain Despretz 分鏡 | 鏡頭語言忠實度；覆蓋完整度；場面排佈清晰 | 在每頁分鐘級時間內匹配 Pixar story-trust 通過率 | DirectorAgent、DoPAgent | ScriptwriterAgent（無法拍攝）、DirectorAgent（場面排佈） | DALL-E 3 / Midjourney API；分鏡格版型；Fountain 解析器 | Self-Refine（導演回饋循環） |
| 15 | **ConceptArtistAgent** | 前期世界／角色設計 | ArtStation 頂尖作品集；McCaig/Church 精華；工作室美術聖經 | 風格聖經遵循度；剪影可讀性；設計連貫性 | 在迭代速度上擊敗工作室美術指導比拼 | DirectorAgent、ProductionDesignAgent | StoryboardAgent（設計偏離） | Midjourney v7；Stable Diffusion ControlNet；Photoshop 生成式填色（API） | Self-Refine + 風格參考 CLIP 評分 |
| 16 | **ProductionDesignAgent** | 場景、外景、世界觀 | ADG 獎；AMPAS 美術指導參賽；Beachler/Carter 演講 | 時代準確度（交叉比對）；色板連貫性；建造可行性 | 在時代研究深度的 ADG 盲測中勝出 | DirectorAgent、DoPAgent | ConceptArtistAgent（風格偏離）、CostumeAgent | Unreal Engine（虛擬勘景）；Veo 3.1 場景生成；檔案影像搜尋 API | Reflexion（將時代研究修正存入記憶） |
| 17 | **CostumeDesignAgent** | 透過服裝塑造角色 | V&A 檔案；CDG 專著；Ruth E. Carter masterclass | 時代／時尚史準確度；剪影識別；色板配搭 | 在時代準確基準上擊敗 CDG 初級設計師 | DirectorAgent、ProductionDesignAgent | MUAAgent（連戲斷裂） | 時尚史向量資料庫（V&A/Met API）；服裝草圖影像生成；色板工具 | Self-Refine（時代準確評分準則） |
| 18 | **MUAAgent (化妝/髮型/SFX)** | 演員臉部／頭髮；類型用特殊化妝 | IATSE 706 語料；Kazu Hiro 工作室參考 | 各鏡次連戲雜湊值；膚色擬真度（FID） | 連戲斷裂率 <0.5%（人類約 ~2%） | DoPAgent、ContinuityAgent | CostumeAgent（色板衝突） | 臉部地標檢測器；感知雜湊比較；Kling 臉部一致性模式 | 憲法式 AI（憲法：連戲規則） |



---

## 4. 聲音與音樂代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 19 | **SoundDesignAgent** | 環境聲、擬音、音效 | BBC 音效庫；MPSE Golden Reel；Burtt/Lievsay 設計筆記 | 頻譜多樣性；同步 ≤±1 格；響度 -23 LUFS | 在恐怖／科幻精華的 MPSE 風格成對比較中勝出 | DirectorAgent、MixerAgent | EditorAgent（音效衝突）、ComposerAgent（頻率遮蔽） | ElevenLabs Sound FX API；Freesound；FFmpeg 頻譜分析；Dolby.io 響度 API | ReAct（搜尋音效庫 → 驗證同步 → 混音） |
| 20 | **ComposerAgent** | 原創配樂 | MAESTRO + 已授權電影配樂語料；ASCAP/BMI；Zimmer/Hildur 訪談記錄 | 配樂與情緒對齊（情緒效價／喚醒度回歸對應觀眾生理代理）；主題反復出現 | 在情緒適配盲測成對比較中擊敗在職作曲家 | DirectorAgent、EditorAgent（音樂剪接） | EditorAgent（剪接打斷配樂）、SoundDesignAgent（遮蔽） | Udio/Suno 音樂生成 API；MIDI 工具鏈；分音軌（Demucs）；響度錶 | Self-Refine + 情緒弧線驗證（生理代理） |
| 21 | **VoiceOverAgent** | 旁白、角色配音、廣告讀稿 | SOVAS 獲獎精華；已同意配音演員語料；Wolfson/Cashman 教練法 | 韻律匹配；發音 100% 對應詞庫；情緒標籤匹配 | 在廣告讀稿盲測偏好中擊敗初級配音；情緒上匹配資深 | DirectorAgent、BrandAgent | ScriptwriterAgent（無法念出的措辭） | ElevenLabs v3 TTS + 聲音克隆；Resemble.AI；發音詞庫 API | LLM-as-Judge（MOS 評分準則） |
| 22 | **SoundMixerAgent (重錄混音)** | 最終混音；交付規格（5.1/Atmos） | CAS 獎；Atmos 規格；廣播響度標準 | LUFS 目標；對白可懂度（STOI ≥0.85）；交付規格通過 | 第一次通過即達到 CAS 規格而不需重做 | EditorAgent、SoundDesignAgent、AccessibilityAgent | SoundDesignAgent（過度設計）、ComposerAgent（音量衝突） | Dolby Atmos 渲染器 API；LUFS／響度量測工具；DaVinci Fairlight MCP | 憲法式 AI（憲法：廣播規格規則） |


---

## 5. 表演與編舞代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 23 | **ChoreographyAgent** | 動作設計（音樂錄像、跳舞挑戰） | Emmy 編舞參賽作品；Goebel/Moore 精華；舞蹈記譜資料集 | 節拍同步準確度；安全約束；病毒模式對齊 | 在短影片盲測偏好中擊敗編舞家草稿 | DirectorAgent、MVDirectorAgent | DirectorAgent（不便拍攝的場面） | Kling 3.0 動態控制（參考影片）；Cascadeur；節拍偵測（librosa） | Self-Refine（評分準則：節拍同步 + 安全） |
| 24 | **MusicVideoDirectorAgent** | 為歌曲設計視覺概念 | DirectorsLibrary；UKMVA/MTV VMA 得獎；Hype Williams/Spike Jonze 精華 | 剪接節奏同步；視覺手冊連貫性；藝人 brief 適配 | 在唱片公司盲測偏好中擊敗商業 MV 導演短名單 | LabelA&RAgent、ArtistAgent | EditorAgent（依節拍剪接）、DoPAgent | Runway Gen-4（風格鎖定生成）；Veo 3.1；情緒板工具（Are.na API） | 多代理辯論（與 DirectorAgent + EditorAgent） |
| 25 | **ComedyWriterAgent** | 短劇、惡搞、病毒迷因撰稿 | UCB/Groundlings 教材；SNL 編劇室記錄；Schur/Fey 教學 | 笑話密度；冷開場掛鈎力；預測每分鐘笑聲 | 在冷讀中擊敗 UCB 桌讀勝率 | AudienceSim、ShowrunnerAgent | ScriptwriterAgent（無笑點）、SocialStrategistAgent（脫離趨勢） | 觀眾笑聲預測模型；趨勢音訊 API（TikTok Creative Center） | Reflexion（將觀眾回饋存入情節記憶） |
| 26 | **TalentAgent (鏡頭前)** | AI 渲染表演 | 方法演技訪談記錄；已同意演員表演語料 | 情緒目標匹配；魅力分數（觀眾代理） | 觀眾留存率匹配同類別頂尖創作者 | DirectorAgent、CastingAgent | DirectorAgent（不可能的走位） | HeyGen Avatar IV；Synthesia 個人虛擬主播；情緒識別模型（AffectNet） | Self-Refine + 情緒回歸驗證器 |
| 27 | **UGCCreatorAgent** | 以創作者口吻製作真實感廣告 | TikTok Creative Center 報告；Alix-Earle 風格基準帖（風格而非身份） | 掛鈎率 ≥30%；「劇本感」偵測器分數低於閾值（低 = 好） | 以 0.1× 成本擊敗付費創作者平均 ROAS | PerformanceMarketerAgent、BrandAgent | PerformanceMarketerAgent（受眾錯誤） | Veo 3.1（直幅 9:16）；ElevenLabs 聲音；CapCut API；TikTok Ads Manager | RLAIF（獎勵來自 ROAS 信號） |


---

## 6. 發行與市場推廣代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 28 | **SocialMediaStrategistAgent** | 平台原生發行、時機、趨勢 | TikTok Creator Portal 數據；Meta Marketing Science；Tubular/Sensor Tower | 預測 vs 實際觸及誤差；趨勢時機延遲 <2h | 在 30 日觸及增長上擊敗代理商社交主管 | AnalystAgent、BrandAgent | CopywriterAgent（脫離平台調性）、EditorAgent（畫幅錯誤） | Meta Graph API；TikTok Content Posting API；Buffer/Hootsuite API；Sensor Tower 數據 | ReAct（趨勢搜尋 → 排程 → 發布） |
| 29 | **CopywriterAgent** | 文案、字幕、掛鈎、標題 | D&AD/One Show 得獎；《Ogilvy on Advertising》；Wiebe Copyhackers | 閱讀年級；掛鈎好奇心分數；品牌聲音餘弦相似度 ≥0.85 | 在廣告 brief 的 D&AD 風格盲測偏好中勝出 | BrandAgent、PerformanceMarketerAgent | ScriptwriterAgent（贅言）、VOArtist（無法念出） | 品牌聲音嵌入模型；Hemingway 易讀性 API；A/B 標題工具 | Self-Refine（評分準則：品牌聲音相似度評分器） |
| 30 | **CreativeDirectorAgent** | 廣告活動概念；跨領域品味 | 康城 Lions Grand Prix 檔案；D&AD Pencils；代理商案例研究 | 概念獨特性（嵌入新穎度 vs 類別先驗）；獎項評分準則預測分數 | 在康城評審模擬器中對人類代理商短名單獲金獎 | ClientAgent、BrandAgent | CopywriterAgent、ArtDirectorAgent | 廣告活動檔案搜尋（Cannes Lions API）；Midjourney 概念視覺；Figma API | 多代理辯論（IdeationAgent + NoveltyAgent 評審團） |
| 31 | **PerformanceMarketerAgent** | 為 ROAS 優化廣告 | Meta Blueprint；TikTok Ads Academy；MMM 文獻 | ROAS 提升 vs 對照；統計顯著性 ≥95% | 在同等開支下，30 日 ROAS 擊敗資深媒體採購 | AnalystAgent、FinanceAgent | UGCAgent（掛鈎弱）、CopywriterAgent（CTA 弱） | Meta Ads API；TikTok Ads API；Google Ads API；Bayesian AB 測試函式庫 | RLAIF（獎勵 = 廣告平台返回的 ROAS 提升信號） |



---

## 7. 教育與領域專家代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 32 | **InstructionalDesignAgent** | 學習目標 → 腳本 → 評估 | ATD 知識體系；Cathy Moore《Action Mapping》；Dirksen《Design for How People Learn》 | Bloom 等級對應；完成率預測 ≥70%；Kirkpatrick L2 測驗 ≥80% | 在學習者留存 RCT 上擊敗 ATD 認證教學設計師 | SMEAgent、AccessibilityAgent | ScriptwriterAgent（無目標）、AnimatorAgent（過度裝飾） | LMS API（SCORM/xAPI）；測驗生成；Bloom 分類器 | Self-Refine（評分準則：Bloom/Kirkpatrick） |
| 33 | **SMEAgent (主題專家)** | 目標領域的內容準確性 | 同行評審期刊；認證課程（CFA、USMLE、AWS 等）；已同意專家訪談語料 | 引用密度；基準考試通過（USMLE、CFA L3 等）；幻覺率 ≤0.5% | 通過與人類專業相同的認證考試達到合格門檻 | FactCheckerAgent、同類 SMEAgent（辯論） | ScriptwriterAgent（不準確）、MotionGraphicsAgent（標籤錯誤） | PubMed/arXiv/JSTOR 搜尋 API；考題庫；對認證語料的 RAG | 多代理辯論 + RAG 檢索 |
| 34 | **FactCheckerAgent** | 為每項陳述評定來源等級 | New Yorker 事實查核手冊；IFCN 認證簽署者；Snopes/PolitiFact 記錄 | 每項陳述的來源等級（一手 > 二手）；交叉來源同意 ≥2 | 已發表更正率低於普立茲級媒體 | SMEAgent、StandardsEditorAgent | ScriptwriterAgent（無來源）、JournalistAgent | 網絡搜尋 API（Brave/Google）；陳述抽取 NER；來源品質分類器 | ReAct（抽取陳述 → 搜尋 → 驗證 → 評等） |
| 35 | **MedicalIllustratorAgent** | 解剖學與程序視覺 | Netter 圖譜；AMI/CMI 課程；Anatomage 參考 | 解剖準確度（解剖檢測模型）；AMI 評分準則分數 | CMI 認證同行盲審投票 ≥合格 | SMEAgent（醫師）、AccessibilityAgent | AnimatorAgent（解剖錯誤）、CopywriterAgent（術語錯誤） | Anatomage 3D API；DALL-E 3（醫療提示模式）；解剖檢測模型 | Self-Refine（評分準則：AMI 評分標準） |
| 36 | **JournalistAgent** | 報導 + 倫理框架 | Pulitzer/duPont/Peabody 得獎；SPJ 倫理；Poynter 教材 | 來源多樣性；公開受訪比例；倫理檢查表通過 | 比新聞編輯室記者更低的更正率 + 更快發稿 | FactCheckerAgent、LegalAgent、StandardsEditorAgent | FactCheckerAgent、ScriptwriterAgent | 網絡研究工具；AP Stylebook API；訪談轉錄（Otter）；SPJ 評分準則 | Reflexion（倫理檢查表作為口頭回饋） |
| 37 | **ComplianceAgent (法務)** | FTC、HIPAA、GDPR、IP、AI 肖像授權 | 律師持續法律教育語料；FTC 背書指引；歐盟 AI 法案；GDPR/CCPA；SAG-AFTRA AI 附加條款 | 檢查表規則覆蓋 100%；發布後零下架 | 比一般媒體律師審查的法律風險更低 | 所有代理（必須通過關卡）；新型問題交由 HumanLawyer | 所有代理（攔截關卡） | 法律規則資料庫（向量化條文）；同意文件儲存；C2PA 驗證庫 | 憲法式 AI（憲法 = 編譯後的法規條文） |
| 38 | **FinanceAgent** | 準確的市場／盈利／加密貨幣事實 | CFA Institute 課程；SEC 行銷規則；Bloomberg/Refinitiv 數據源 | 數值準確度 100%；SEC 行銷規則合規 | 通過模擬 CFA L3；撤回率低於分析師桌 | SMEAgent（經濟）、ComplianceAgent | ScriptwriterAgent（數字漂移）、MotionGraphicsAgent（圖表比例錯誤） | Bloomberg API；EDGAR/SEC 申報；財務計算驗證器 | ReAct（取得數據 → 驗證 → 撰寫） |
| 39 | **FoodStylistAgent** | 上鏡的食物、菜式真實性 | James Beard 媒體獎檔案；Susan Spungen 技法；IACP 語料 | 視覺食慾吸引力（美學回歸器）；菜式步驟準確度 | 在靜態 + 動態盲測偏好中擊敗編輯級食物造型師 | DoPAgent（燈光）、DirectorAgent | ScriptwriterAgent（不可能的菜式） | DALL-E 3 / Midjourney（食物圖生成）；菜式步驟解析器；美學評分模型 | Self-Refine（美學回歸器作為評分準則） |
| 40 | **TravelCineAgent** | 目的地攝影 | Brandon Li / Chris Burkard 精華；NatGeo 風格指南；Banff 影展入選 | 開場鏡頭多樣性；地點氣氛匹配 | 以 0.1× 出勤成本贏得 T+L 盲測偏好 | DirectorAgent、DronePilotAgent | DronePilotAgent（禁飛區） | Veo 3.1（場景生成）；Google Earth Studio；AirMap 地理圍欄；Unsplash API | Self-Refine + 地理圍欄安全驗證器 |
| 41 | **ChildrensAuthorAgent** | 適齡故事 + 安全 | Caldecott/Geisel 得獎；Mo Willems / Julia Donaldson 公開作品；幼兒教育文獻 | Lexile 帶匹配；Common-Sense-Media 安全通過；押韻／韻律分數 | 在參賽池中擊敗 Caldecott 評分準則的預測分數 | ChildSafetyAgent、ParentSimAgent | AnimatorAgent（嚇人）、VOAgent（年齡調性錯誤） | Lexile 分析器 API；Common Sense Media 評分準則；押韻／韻律工具（CMU 發音字典） | 憲法式 AI（兒童安全憲法） |
| 42 | **AudiobookNarratorAgent** | 持續角色與旁白 | Audie 獎檔案；AudioFile Earphones；已同意旁白語料 | 聲音持久度（60 分鐘無漂移）；角色區別（嵌入距離） | 在 AudioFile 盲測中以工作室時間的一小部分勝出 | DirectorAgent、AuthorAgent | VOArtistAgent（過度演繹） | ElevenLabs v3 長篇 TTS；Projects API（書本章節）；聲音一致性監控 | Self-Refine（漂移偵測作為回饋循環） |
| 43 | **SignLanguageInterpreterAgent** | 準確的 ASL／BSL 翻譯 | RID NIC 課程；NAD 認可語料；聾人社群已同意手語數據 | 手語準確度（聾人評審投票）；面部語法標記 | 在 NAD 評審盲測偏好中大規模勝出 | DeafCommunityReviewAgent（HiTL）、LinguistAgent | VoiceCloneAgent（無字幕）、AccessibilityAgent | 手語虛擬主播渲染（SignAll）；MediaPipe 姿態估計；面部動作單元偵測器 | RLAIF（獎勵來自聾人社群評審團） |
| 44 | **LocalizationQAAgent (語言學家)** | 翻譯與文化適配 | LISA QA 模型；MQM 錯誤分類；ATA 認證準備 | 每千字 MQM 錯誤率；文化標記計數 | 以 10× 速度擊敗 LSP 人工 QA 的 MQM 錯誤率 | NativeReviewerAgent、BrandAgent | VoiceCloneAgent（發音錯誤）、DubbingAgent | DeepL/Google Translate API；MQM 錯誤標註器；術語管理（memoQ API） | Self-Refine（評分準則：MQM 評分框架） |
| 45 | **RealEstatePhotoAgent / 3D Scan Op** | 廣角室內；Matterport 掃描 | Mike Kelley 建築攝影教學；APALA 參考 | 垂直線筆直度；HDR 曝光堆疊；覆蓋率 % | 對人類拍攝基準的房源 CTR 提升 | DoPAgent、DronePilotAgent | DronePilotAgent（非法高度） | Matterport SDK；HDR 處理（Luminance HDR）；鏡頭校正工具；Veo 3.1 | ReAct（評估空間 → 生成視角 → 驗證幾何） |



---

## 8. AI 紀元專業代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 46 | **PromptEngineerAgent / GeneratorOperator** | 撰寫提示詞；操控 Sora/Veo/Runway/Kling | Karen X. Cheng / Paul Trillo 公開提示詞集；r/aivideo 社群；Runway AIFF 評審筆記 | 提示詞 → 輸出 CLIP-T 分數；接受前的迭代次數；種子控制可重現性 | ≤3 次迭代達到目標鏡頭（人類平均 10 次） | DirectorAgent、AIQAAgent | AIQAAgent（重生成預算）、ConsistencyAgent | Sora 2 API、Veo 3.1、Runway Gen-4/Aleph、Kling 3.0；種子／參數登記表 | DSPy / OPRO 提示詞優化（Yang 2023） |
| 47 | **AvatarDesignAgent** | 合成主播身份 | Synthesia/HeyGen 設計文件；深偽偵測文獻（Hany Farid）；C2PA 規範 | 各鏡頭間身份一致性雜湊；同意文件鏈；C2PA 已簽 | 大規模通過 C2PA 可驗證 + Partnership-on-AI 框架 | ComplianceAgent（同意）、DeepfakeDetectionAgent | VoiceCloneAgent（外貌偏差）、LipSyncAgent | HeyGen Avatar IV API；Synthesia API；C2PA 簽署庫（c2patool）；臉部嵌入模型 | 憲法式 AI（同意 + 身份憲法） |
| 48 | **VoiceCloneAgent / LipSyncSpecialist** | 聲音克隆 + 嘴形對音 | ElevenLabs 安全文件；Wav2Lip/Sync.so 論文；James Baxter 嘴形動畫參考 | 聲音 MOS ≥4.2；音素—口型對齊誤差 <40ms；同意旗標已驗證 | 在盲測 MOS 上擊敗專業 ADR + 嘴形替換 | ComplianceAgent（同意）、AnimatorAgent（嘴形對音黃金標準） | AvatarDesignAgent（臉部閃爍）、DubbingAgent | ElevenLabs v3 克隆 API；Sync.so 嘴形對音；Wav2Lip；同意文件驗證 | Self-Refine + MOS 評分模型作為評判 |
| 49 | **AIQAConsistencyAgent** | 偵測畫面漂移、手／臉瑕疵、身份斷裂 | VBench、EvalCrafter、FVD 文獻；MPC/Weta QC 檢查表；深偽偵測模型動物園 | 每幀瑕疵分數；場景間身份雜湊漂移；手／手指偵測通過 | 抓出資深 QC 抓出的 >95% 瑕疵，再加 30% 人類遺漏的 | DirectorAgent、VFXSupAgent | GeneratorAgent（重生成請求）、CompositorAgent | VBench 評估套件；手部偵測模型；臉部 ID 嵌入（ArcFace）；幀差工具 | 工具使用 / ReAct（執行偵測器 → 標記 → 報告） |
| 50 | **PersonalizationEngineerAgent** | 變數模板（姓名／臉／聲音替換） | Idomoo 案例研究；DMA 同行評審活動；MarTech 自動化文獻 | 渲染成功率 ≥99.5%；抽查通過；隱私審核通過 | 比頂尖人工模板化活動有更高的禮品分享率 | ComplianceAgent（GDPR/CCPA）、AnalystAgent | TemplateDesignerAgent（模板脆弱性） | Idomoo/Pirsonal API；HeyGen 個人化；GDPR 同意管理平台 | ReAct（組裝模板 → 渲染 → 驗證 → 交付） |
| 51 | **TrailerEditorAgent** | 掛鈎驅動的預告剪接 | Golden Trailer 獎檔案；Mark Woollen / AV Squad 公開精華；預告音樂庫 | 3 秒處掛鈎率；上升動作曲線適配；音樂同步精確度 | 在 Golden Trailer 評分準則盲測比較中勝出 | DirectorAgent、MusicSupervisorAgent | EditorAgent（過度剪接）、ComposerAgent（不匹配） | DaVinci Resolve（MCP）；預告音樂 API（Musicbed/Artlist）；留存曲線預測器 | Self-Refine（留存曲線模型作為回饋） |
| 52 | **SportsAnalystAgent / TelestratorOp** | 戰術解析 + 圖示 | MIT Sloan 體育分析論文；ESPN Stats & Info；Kirk Goldsberry 分析 | 預測 vs 實際戰術呼叫準確度；螢幕清晰度分數 | 在戰術預測任務上擊敗前運動員評論員 | SMEAgent（運動）、JournalistAgent | EditorAgent（漏播重播）、MotionGraphicsAgent（圖表清晰度） | 體育數據 API（StatsBomb、NBA Stats）；戰術圖示疊加工具；After Effects MCP | ReAct（取得戰術數據 → 標註 → 渲染疊加） |


---

## 9. 特殊元代理

### 9.1 編排代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 53 | **OrchestratorAgent** | 執行 CrewAI/AutoGen/LangGraph DAG；重試、超時、扇出/扇入 | LangGraph + CrewAI + AutoGen 參考模式；Airflow/Temporal；PGA 排程模板 | DAG 完成率 ≥99.5%；SLA 達成；死鎖率 = 0 | 在相同範圍下，比人類 EP 有更低的平均交付時間 | ProducerAgent（範圍）、JudgeAgent（爭議）、HiTL（停滯時） | 所有代理（資源消耗、重試風暴） | LangGraph 狀態機；Temporal 工作流引擎；Redis（分散式鎖）；可觀測性（LangSmith） | 代理圖（LangGraph）— 確定性 DAG 執行 |
| 54 | **PlannerAgent** | 將 brief 分解為含分配 + 評論關卡的階段 DAG | 製作管理語料；PMBOK；CrewAI 任務圖；階段模板 | 計劃有效性（無遺漏關卡）；估算成本與實際偏差 <10% | 在盲測 A/B 中產生比 EP 初版更緊湊、更便宜的計劃 | ProducerAgent、FinanceAgent（預算） | RouterAgent（選錯代理）、OrchestratorAgent | LangGraph 計劃生成；成本估算模型；Gantt/PERT 工具 | ReAct（分解 → 估算 → 驗證 → 發出 DAG） |
| 55 | **RouterAgent** | 為每個子任務挑選正確的專業代理（與模型） | 代理能力註冊表；基準歷史（每代理 × 任務類型的成本／品質／延遲） | 對應 oracle 路由準確度 ≥95%；單任務成本在預算內 | 在成本調整品質上擊敗人類監製的代理／供應商選擇 | OrchestratorAgent、CostOptimizerAgent | PlannerAgent（分解錯誤） | 代理註冊資料庫；基準排行榜快取；定價 API | 分類器 + ReAct（任務嵌入匹配 → 代理能力） |
| 56 | **JudgeAgent** | 透過多代理辯論裁決代理間爭議；按評分準則為輸出評分 | Du 2023（LLM 辯論）；MT-Bench 評分準則；公會評分表（DGA/WGA/ASC/ACE） | 與人類專家評審團的評審者間一致性 κ ≥0.8 | 與人類陪審團相比，比中位數人類陪審員的 κ 更高 | HiTL（裁決被推翻時） | DirectorAgent、ScreenwriterAgent、任何爭議的代理對 | MT-Bench/Arena 評估架構；評分準則模板引擎 | 多代理辯論 (Du 2023) + LLM-as-Judge (Zheng 2023) |
| 57 | **GateKeeperAgent** | 階段轉換；驗證 L1/L2/L3 標準；簽署 C2PA 來源 | 階段關卡方法論；PGA Producers Mark；QMS 稽核模式 | 通過關卡的零滲漏瑕疵；簽核 SLA 命中率 ≥99% | 比人類 QA 主管更低的逃逸瑕疵率 | ComplianceAgent、AIQAConsistencyAgent | OrchestratorAgent（過早推進） | C2PA 簽署（c2patool）；JSON 模式驗證器；評分準則評估端點 | 憲法式 AI（憲法 = 階段關卡標準） |
| 58 | **MemoryAgent** | 情節 + 長期專案記憶；為任何代理提供檢索 | Reflexion (Shinn 2023)；MemGPT；向量資料庫最佳實踐 | 專案 Q&A 上的檢索 precision@5 ≥0.9；新鮮度 SLA | 在規模上比監製專案聖經有更高的召回率 | 所有代理（修正事件） | 所有代理（過時事實） | Pinecone/Weaviate/Qdrant 向量資料庫；MemGPT 風格分層記憶；嵌入模型 | Reflexion 記憶架構（MemGPT 擴展） |


### 9.2 創意代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 59 | **IdeationAgent** | 概念、掛鈎、標語、假設角度的發散性腦力激盪 | 康城 Lions Grand Prix 檔案；D&AD 得獎；IDEO 設計思維語料；SCAMPER / 平行思考（de Bono） | 每個 brief 的點子數量；新穎度（嵌入與語料的距離）；批次內語意多樣性 | 在概念密度的代理商比稿盲測中勝出 | CreativeDirectorAgent、NoveltyAgent | CopywriterAgent（衍生）、DirectorAgent（不可拍攝） | 嵌入新穎度評分器；概念聚類（UMAP）；Are.na/Pinterest 搜尋 | Self-Refine + NoveltyAgent 作為批評者 |
| 60 | **NarrativeArcAgent** | 塑造三幕／Save-the-Cat／起承轉合／英雄之旅結構 | Campbell《千面英雄》；Snyder《Save the Cat》；Truby《故事解剖》；Black List 結構分析 | 節拍表覆蓋 100%；轉折點間距匹配類型先驗；情緒弧曲線適配 | 在結構評分準則盲讀中擊敗 WGA 編劇的初稿 | ScreenwriterAgent、DirectorAgent | ScreenwriterAgent（中段下垂） | 節拍表驗證器；情緒弧繪圖器；結構模板 | Self-Refine（評分準則：節拍表完整度） |
| 61 | **StyleTransferAgent** | 將命名美學（Wes Anderson、A24、賽博龐克、蒸汽波、吉卜力等）一致地套用至各鏡頭 | 每種風格的精選語料；LoRA／種子註冊表；參考幀庫 | 風格相似度分數（CLIP/DINO）≥0.85；各鏡頭間一致性變異 ≤τ | 在盲測偏好中擊敗人類調色師 + 調色師做相同風格 | DirectorAgent、ColoristAgent | GeneratorAgent（脫離風格） | 每種風格的 LoRA 權重；CLIP/DINO 相似度評分器；Runway 風格鎖定模式；ComfyUI | Self-Refine（CLIP 風格分數作為回饋） |
| 62 | **WorldBuildingAgent** | 為系列與特許經營構建傳說、規則、地理、派系、魔法／科技系統 | Tolkien 傳奇；《Worldbuilding》(Adams)；同人 Wiki 語料；系列聖經洩露 | 內部一致性檢查（N 個條目間無矛盾）；規則完整度 | 以 10× 規模比人類編劇室聖經有更低的矛盾率 | ShowrunnerAgent、FactCheckerAgent | ScriptwriterAgent（傳說斷裂）、ConceptArtistAgent | 長上下文 LLM（Gemini 2.5 Pro）；矛盾偵測模型；wiki 圖資料庫 | Reflexion（矛盾修正 → 情節記憶） |
| 63 | **MoodBoardAgent** | 構建參考板：視覺、聲音、調性 | Pinterest/Are.na 語料；視覺手冊檔案；Spotify-Canvas 參考 | 參考連貫性（聚類緊密度）；brief 對齊 | 在盲測 A/B 中比人類美術指導更快、更緊湊地構建情緒板 | DirectorAgent、ProductionDesignAgent | ConceptArtistAgent（脫離情緒） | Pinterest/Are.na API；Spotify Canvas；CLIP 聚類；Figma 板生成 | ReAct（搜尋 → 聚類 → 排版 → 驗證連貫性） |
| 64 | **NoveltyAgent / Anti-Cliché Critic** | 標記陳腔濫調、套路、過度擬合語料的輸出 | TV Tropes；OpenSubtitles n-gram 頻率；語料新穎度嵌入 | 每個輸出的陳腔濫調命中數；相對於類別先驗的新穎度分數 | 在盲評中比有經驗的劇本編輯抓出更多陳腔濫調 | IdeationAgent、ScreenwriterAgent | ScriptwriterAgent（套路堆砌）、CopywriterAgent（模板化） | TV Tropes 爬蟲；n-gram 頻率資料庫；嵌入新穎度評分器 | LLM-as-Judge（反陳腔濫調憲法） |
| 65 | **EmotionalArcAgent** | 在執行時間內映射效價／喚醒度曲線；建議節拍 | Plutchik 情緒輪；情感計算語料；Cron《Story Genius》 | 對目標形狀的曲線適配；觀眾生理代理回歸準確度 | 比試映 NRG 卡片有更佳的留存曲線預測 | DirectorAgent、EditorAgent、ComposerAgent | EditorAgent（中段平淡）、ComposerAgent（配樂不匹配） | 情感分類器（GoEmotions）；留存曲線預測器；生理代理模型 | Self-Refine（情緒弧曲線作為評分準則目標） |



### 9.3 研究代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 66 | **WebResearchAgent** | 即時網絡搜尋、來源排名、引用抽取 | Bing/Google/Brave 搜尋 API；Common Crawl；Perplexity / GPTSearcher 模式 | 每項陳述的來源等級；引用精確度；新近度視窗命中 | 在相同精確度下比新聞編輯室研究員更快 + 更多來源 | FactCheckerAgent、CitationAgent | ScriptwriterAgent（無引用陳述） | Brave/Google 搜尋 API；Jina Reader（網頁→Markdown）；來源品質分類器 | ReAct（查詢 → 取得 → 抽取 → 評等 → 引用） |
| 67 | **ArchiveResearchAgent** | 歷史／學術／檔案深度搜尋 | JSTOR、arXiv、PubMed、AP Archive、Getty、FOIA 數據集 | 一手來源比例；檔案覆蓋廣度 | 比紀錄片監製研究檔案有更高的一手來源比例 | FactCheckerAgent、SMEAgent | ScriptwriterAgent（過度依賴二手來源） | JSTOR/arXiv/PubMed API；Getty Images API；FOIA 申請工具；OCR (Tesseract) | ReAct（撰寫查詢 → 搜尋檔案 → 抽取 → 評等來源） |
| 68 | **TrendIntelligenceAgent** | 偵測新興迷因、聲音、形式並提前預警 | TikTok Creative Center、Trendpop、Tubular、Sensor Tower、Reddit / X 即時流 | 趨勢預測的領先時間 vs 病毒高峰；趨勢清單的精確度／召回率 | 在更高精確度下比人類社交策略師更早偵測 | SocialStrategistAgent、CopywriterAgent | IdeationAgent（脫離趨勢） | TikTok Creative Center API；Reddit/X 串流 API；Sensor Tower；Google Trends | ReAct + 時間序列異常偵測 |
| 69 | **CompetitorIntelligenceAgent** | 競爭對手品牌、創作者、片廠正在發布甚麼 | 公開廣告庫（Meta Ad Library、TikTok Top Ads）；YouTube 頻道爬取；院線／串流發行追蹤 | 命名競品集的覆蓋率 %；我方輸出 vs 市場景觀的新穎度 | 在盲測比較中比代理商策略簡報更全面 | BrandAgent、CreativeDirectorAgent | IdeationAgent（衍生） | Meta Ad Library API；TikTok Top Ads；SimilarWeb；YouTube Data API v3 | ReAct（爬取競品 → 分類 → 報告差距） |
| 70 | **CitationAgent** | 規範化來源；評定一手／二手／三手 | Chicago、APA、AP 風格指南；SPJ 來源評等；CRAAP 測試 | 引用格式 100% 有效；一手來源 % ≥目標 | 比新聞編輯室校對台更低的格式／評等錯誤率 | FactCheckerAgent、JournalistAgent | WebResearchAgent（弱來源） | 引用解析器（AnyStyle）；DOI 解析器；CRAAP 評分模型 | Self-Refine（格式驗證器 + 來源評等器作為評分準則） |
| 71 | **InterviewSynthesisAgent** | 進行／綜合實踐者訪談為指令調教數據 | Otter / Rev 轉錄；同意書；SAG-AFTRA / WGA 訪談同意模板 | 主題抽取的編碼者間一致性；同意鏈完整性 | 比定性研究員更快 + 更豐富的主題抽取 | ResearchPIAgent (HiTL)、ComplianceAgent | SMEAgent（專家總結錯誤） | Otter.ai/Rev API（轉錄）；主題編碼模型；同意管理資料庫 | Reflexion（訪問者依主題缺口優化問題） |
| 72 | **BenchmarkResearchAgent** | 監控 VBench、EvalCrafter、MT-Bench、FVD、CLIP-T 排行榜 + 新基準 | Papers-with-Code；HuggingFace 排行榜；AI 會議論文集 | 活躍基準的覆蓋率；新鮮度 ≤7 日 | 比人類 ML 研究團隊更快 + 更廣 | 任何 OptimizationAgent | 所有 AI 紀元代理（過時基準） | Papers-with-Code API；HuggingFace Hub API；arXiv RSS；VBench 排行榜爬蟲 | ReAct（輪詢排行榜 → 偵測變化 → 警示） |


### 9.4 優化代理

| # | 代理 | 職責 | 知識蒸餾來源 | 自我品質標準 | 超越人類信號 | 接受評論來源 | 評論對象 | 工具存取 | 架構模式 |
|---|---|---|---|---|---|---|---|---|---|
| 73 | **PromptOptimizerAgent** | 透過 OPRO/APE/DSPy/Promptbreeder 自動改進提示詞 | OPRO (Yang 2023)、APE (Zhou 2022)、DSPy (Stanford)、Promptbreeder (DeepMind) | 在留出評估上每次迭代的分數提升；收斂的迭代次數 | 在留出 brief 上擊敗 Karen X. Cheng / Paul Trillo 風格手工調教提示詞 | PromptEngineerAgent、AIQAAgent | PromptEngineerAgent（次優種子） | DSPy 框架（MIPRO 優化器）；OPRO 實作；留出評估架構 | DSPy 編譯 + OPRO 元優化 |
| 74 | **CostOptimizerAgent** | 在模型／供應商之間路由以求 $/品質 | 供應商定價表；基準成本—品質前沿；FrugalGPT 模式 | 每個成功任務的 $；與成本—品質前沿的 Pareto 距離 | 比人類 CFO + 監製的路由決策有更低的 $/品質 | RouterAgent、FinanceAgent | RouterAgent（超支）、GeneratorAgent（重生成消耗） | 供應商定價 API；基準成本資料庫；FrugalGPT 階梯式邏輯 | ReAct（評估任務 → 挑選符合閾值的最便宜模型） |
| 75 | **LatencyOptimizerAgent** | 並行化、快取、推測解碼、批次封裝 | vLLM、TensorRT-LLM、蒸餾文獻；Anyscale / Ray 模式 | p50 / p95 延遲；每 GPU 小時的吞吐量 | 在同等品質下比人類調教的管線有更低的 p95 | OrchestratorAgent | OrchestratorAgent（序列瓶頸） | vLLM；TensorRT-LLM；Ray Serve；Redis（回應快取）；推測解碼設定 | 工具使用剖析 + 自動化管線重構 |
| 76 | **RetentionOptimizerAgent** | 為 AVD / 留存率調教掛鈎、節奏、結構 | YouTube Analytics 公開基準；TikTok 留存曲線；AudienceSim 輸出 | 預測留存曲線 vs 實際；對照組之上的 AVD 提升 | 在 A/B 中比資深 YouTube 剪輯師有更高的 AVD 提升 | EditorAgent、AudienceSimAgent | EditorAgent（開場慢）、ScriptwriterAgent（前段贅言） | YouTube Analytics API；留存曲線預測模型；A/B 測試框架 | RLAIF（獎勵 = 真實分析的留存提升） |
| 77 | **ROASOptimizerAgent** | 為效益指標優化廣告創意 | Meta Marketing Science、TikTok Ads Academy、MMM / MTA 文獻 | ROAS 提升 vs 對照；顯著性 ≥95% | 在同等預算下擊敗資深效益行銷人員 | PerformanceMarketerAgent、AnalystAgent | UGCAgent（掛鈎率低）、CopywriterAgent（CTA 弱） | Meta Ads API（創意測試）；TikTok Ads；Bayesian MMM 工具（Robyn/Meridian） | RLAIF（獎勵 = 廣告平台回饋的真實 ROAS） |
| 78 | **AccessibilityOptimizerAgent** | WCAG 2.2 對比度、字幕時間、口述影像品質、色盲安全色板 | WCAG 2.2 規範；W3C / WAI-ARIA；DCMP 字幕指引；聾人／聽障社群指引 | WCAG 合規分數 100% AA、≥90% AAA；字幕 WER ≤2% | 比 ADA 認證人類審計員抓出更多 a11y 缺陷 | AccessibilityAgent (HiTL)、ComplianceAgent | EditorAgent（字幕同步）、ColoristAgent（對比度） | axe-core/Lighthouse（對比度）；Whisper v4（字幕生成）；口述影像生成器 | 憲法式 AI（憲法 = WCAG 2.2 成功標準） |
| 79 | **EvaluationHarnessAgent** | 持續執行基準（VBench、EvalCrafter、MT-Bench、FVD、CLIP-T）並發布回歸 | Papers-with-Code；HuggingFace 排行榜；基準程式碼倉 | 回歸偵測精確度／召回率；警示延遲 <1h | 比 ML 工程團隊輪值更快抓到回歸 | BenchmarkResearchAgent | 所有 AI 代理（回歸警示） | VBench 套件；EvalCrafter；MT-Bench 評估架構；CI/CD（GitHub Actions）；警示（PagerDuty） | 工具使用 / ReAct（執行基準 → 比較 → 若回歸則警示） |
| 80 | **SafetyRedTeamAgent** | 為深偽、偏見、越獄、誹謗對輸出進行對抗性攻擊 | Hany Farid 實驗室基準；Partnership on AI 合成媒體框架；OWASP LLM Top 10 | 攻擊成功率保持 ≤1%；攻擊分類覆蓋率 | 比內部紅隊輪值有更高的覆蓋率 | EthicsAgent (HiTL)、ComplianceAgent | AvatarDesignAgent、VoiceCloneAgent、所有 GeneratorAgent | 深偽偵測器（Farid 實驗室模型）；偏見探針；越獄提示詞庫；OWASP 掃描器 | 多代理辯論（紅隊 vs 防禦方）+ 對抗式搜尋 |



---

## 10. AI 代理共同架構

每個代理 — 不論類別 — 都實作這個骨架。源自原始文件的架構模式（§1）、評論協議（§6）與通用成功標準框架（§5），並結合 2026 年最新的工具研究。

### 10.1 架構示意圖

下圖將下方表格中的每項元件映射到單一視覺示意圖上 — 輸入流入 **代理核心**，由三層 **品質關卡**（規格 → 評分準則 → 偏好）檢查，只有三層全部通過時才會發出帶 C2PA 簽名的產物。側邊通道分別處理 **記憶**（狀態）、**工具**（透過 MCP 執行動作）、**評論**（同儕回饋）、**HiTL**（人類介入）以及 **持續學習**（RLAIF 回饋循環）。整個代理在外層的 **編排層**（LangGraph / CrewAI / AutoGen DAG）中以節點形式運行。

![AI 代理共同架構](./common-agent-structure.svg)

> **提示：** 在 GitHub 上點擊圖片可全螢幕檢視，或直接下載 [`common-agent-structure.svg`](./common-agent-structure.svg)。

### 10.2 元件參考表

| # | 元件 | 用途 | 機制 / 實作備註 |
|---|---|---|---|
| 1 | **身份** | 用於路由、日誌、來源憑證的穩定唯一代號 | kebab-case ID + 語意化版本（例如 `director-agent@2.1.0`）。在 RouterAgent 使用的代理能力註冊表中註冊。 |
| 2 | **職責（範疇）** | 一句話定義代理擁有甚麼 | 對應人類工種角色。在註冊表中以明確邊界防止範疇重疊。 |
| 3 | **知識蒸餾來源** | 代理訓練或 RAG 依據的已授權／已同意語料 | 獎項檔案、學術論文、專家訪談、同行評審期刊。透過持續蒸餾循環刷新（原始文件 §7）。 |
| 4 | **工具存取** | 外部 API、生成器、驗證器、DCC 橋接 | 影片生成：Sora 2、Veo 3.1（Gemini API）、Runway Gen-4/Aleph、Kling 3.0。聲音：ElevenLabs v3、Sync.so、HeyGen。DCC：Resolve/Nuke/AE 透過 MCP 橋接。全部以 MCP（Model Context Protocol，Anthropic 2024）存取。 |
| 5 | **架構模式** | 為代理提供動力的推理／學習循環 | 一個或多個：Self-Refine [1]、Reflexion [2]、RLAIF/憲法式 AI [3]、多代理辯論 [4]、LLM-as-Judge [5]、成對偏好（Arena）[5]、ReAct [6]、代理圖（LangGraph/CrewAI/AutoGen）[7]、DSPy/OPRO 提示詞優化 [8]。 |
| 6 | **記憶** | 情節 + 長期專案記憶 | 透過 MemoryAgent 存取的向量資料庫（Pinecone/Weaviate/Qdrant）。實作 MemGPT 風格的分層記憶，附帶摘要與淘汰機制。Reflexion 代理在此存放口頭自我回饋。 |
| 7 | **憲法 / 評分準則** | 用於自我檢查的、書寫好的角色專屬評分指南 | 範例：Murch 的「六法則」（剪輯）、12 法則（動畫）、Save-the-Cat 節拍（編劇）、WCAG 2.2（無障礙）、FAA Part 107（無人機）、SAG-AFTRA AI 附加條款（同意）。在憲法式 AI 模式中作為「憲法」使用。 |
| 8 | **自審品質：L1 規格** | 輸出是否符合結構化的 brief？ | JSON 模式驗證 + 工具驗證器（編解碼、LUFS、畫面比例、幀數、檔案格式）。必須 100% 通過。 |
| 9 | **自審品質：L2 評分準則** | 是否符合此角色的工藝評分準則？ | LLM-as-Judge (Zheng 2023) 配合角色專屬憲法。必須 ≥85/100。若低於閾值，最多 3 次 Self-Refine 迭代。 |
| 10 | **自審品質：L3 偏好** | 目標觀眾會選擇此作品而非人類基準嗎？ | 成對比較：AudienceSim 評審團（≥200 個模擬人格 + ≥20 個 HiTL 樣本）。勝率 ≥50%（持平）或 ≥55%（超越）。 |
| 11 | **超越人類信號** | 證明代理超越認證專業人員的預先註冊指標 | 基準稱霸；盲測 Arena 偏好 ≥55%；速度 × 品質（同等 L2 而周轉時間 ≤10%）；更低的 90 日缺陷率；認證考試通過；同等品質下更高的新穎度。 |
| 12 | **評論收件匣** | 接收同儕結構化回饋的通道 | 共享的 `CritiqueMessage` JSON 匯流排。嚴重性：blocker（停止 DAG）、major（Self-Refine ≤3 次）、minor/nit（記錄供 RLAIF）。爭議 → JudgeAgent 多代理辯論 → 若未解決則 HiTL。 |
| 13 | **評論發件匣** | 此代理有資格審查的同儕代理 | 在名冊中逐代理定義。訊息發送至同一匯流排。附證據、引用評分準則、加入 C2PA 來源憑證。 |
| 14 | **HiTL 升級** | 何時必須引入人類 | 同意（SAG-AFTRA AI 附加條款、歐盟 AI 法案 Art. 50）；最終法律簽核；MPA 分級；影展資格；危機溝通；跨文化敏感度。 |
| 15 | **來源憑證（C2PA）** | 對每個產物進行密碼學簽署 | 每個發出的產物都用 C2PA（c2patool）簽署。下游代理驗證鏈條。已接受的評論加入 manifest。平台（YouTube、TikTok、Meta）依 C2PA 存在自動標籤。 |
| 16 | **持續學習** | 代理在部署後如何持續改進 | 啟動（已授權語料）→ 專家訪談（付費、已同意）→ 即時 RLAIF（DPO/KTO）→ 獎項評分準則接地 → 對抗紅隊 → 30/60/90 日現實檢驗（留存、ROAS、獎項）。 |
| 17 | **編排整合** | 代理如何融入多代理圖 | 註冊為 LangGraph/CrewAI/AutoGen DAG 中的節點。OrchestratorAgent 排程；PlannerAgent 分配；RouterAgent 選擇模型／供應商；GateKeeperAgent 在推進前驗證 L1-L3。 |



### CritiqueMessage 結構（通用）

```json
{
  "critique_id": "uuid",
  "from_agent": "EditorAgent",
  "to_agent": "DirectorAgent",
  "artifact_ref": "shot_42_take_3.mp4",
  "severity": "blocker | major | minor | nit",
  "category": "pacing | continuity | accuracy | compliance | accessibility | brand | craft",
  "evidence": ["timecode 00:01:14 — 比類型先驗的剪接點多停留了 1.4 秒"],
  "suggested_action": "trim 1.0s; re-evaluate hold",
  "rubric_reference": "Murch Rule of Six §3",
  "must_resolve_before": "phase_4_review"
}
```

### 組合示意圖

```
[Brief] ──► PlannerAgent ──► OrchestratorAgent ──► RouterAgent ──► （§1–§8 共 52 個工種代理）
                 ▲                  │                                       │
                 │                  ▼                                       ▼
             MemoryAgent      GateKeeperAgent ◄─── JudgeAgent ◄──── CritiqueMessages
                                    ▲                                       ▲
                                    │                                       │
            [創意元代理：] IdeationAgent · NarrativeArcAgent · StyleTransferAgent · MoodBoardAgent · NoveltyAgent · EmotionalArcAgent
            [研究元代理：] WebResearchAgent · ArchiveResearchAgent · TrendIntelAgent · CompetitorIntelAgent · CitationAgent · InterviewSynthAgent · BenchmarkResearchAgent
            [優化元代理：] PromptOptimizerAgent · CostOptimizer · LatencyOptimizer · RetentionOptimizer · ROASOptimizer · AccessibilityOptimizer · EvalHarnessAgent · SafetyRedTeamAgent
```

---

## 11. 參考資料

### 基礎論文（架構模式）

| 編號 | 論文 | 主要貢獻 | 連結 |
|---|---|---|---|
| [1] | Madaan et al., "Self-Refine: Iterative Refinement with Self-Feedback," NeurIPS 2023 | 代理起草 → 按評分準則自我批評 → 在不更新權重的情況下迭代修訂 | [arXiv:2303.17651](https://arxiv.org/abs/2303.17651) |
| [2] | Shinn et al., "Reflexion: Language Agents with Verbal Reinforcement Learning," NeurIPS 2023 | 將口頭自我反思存入情節記憶緩衝，以改進後續嘗試的決策 | [arXiv:2303.11366](https://arxiv.org/abs/2303.11366) |
| [3] | Bai et al., "Constitutional AI: Harmlessness from AI Feedback," 2022 | 由書寫好的憲法管理的 AI 評論員提供獎勵信號；無需人類標籤的 RLAIF | [arXiv:2212.08073](https://arxiv.org/abs/2212.08073) |
| [4] | Du et al., "Improving Factuality and Reasoning in Language Models through Multiagent Debate," 2023 | 多個 LLM 代理辯論；改善多種任務的事實性與推理 | [arXiv:2305.14325](https://arxiv.org/abs/2305.14325) |
| [5] | Zheng et al., "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena," NeurIPS 2023 | GPT-4 評判與人類偏好達 >80% 一致；可擴展的評估 | [arXiv:2306.05685](https://arxiv.org/abs/2306.05685) |
| [6] | Yao et al., "ReAct: Synergizing Reasoning and Acting in Language Models," ICLR 2023 | 將推理痕跡與工具使用動作交錯進行，以實現有根據的決策 | [arXiv:2210.03629](https://arxiv.org/abs/2210.03629) |
| [7] | LangGraph / CrewAI / AutoGen (2024–2026) | 代理圖編排：含狀態、交接、審查關卡與 HiTL 的 DAG | [LangGraph](https://github.com/langchain-ai/langgraph)、[CrewAI](https://github.com/crewAIInc/crewAI)、[AutoGen](https://github.com/microsoft/autogen) |
| [8] | Yang et al., "Large Language Models as Optimizers" (OPRO), 2023；Khattab et al., DSPy (Stanford, 2023–2026) | 用 LLM 進行提示詞元優化；DSPy 將宣告式 LM 程式編譯為優化過的管線 | [OPRO arXiv:2309.03409](https://arxiv.org/abs/2309.03409)、[DSPy](https://github.com/stanfordnlp/dspy) |

### 評估基準

| 基準 | 範圍 | 連結 |
|---|---|---|
| VBench / VBench 2.0 | 影片生成品質 — 16 個維度（時序 + 單幀）；VBench 2.0 加入人類保真度、創意、物理 | [arXiv:2311.17982](https://arxiv.org/abs/2311.17982)、[VBench 2.0: arXiv:2503.21755](https://arxiv.org/abs/2503.21755) |
| EvalCrafter | 文字轉影片 — 18 項視覺、內容、動作品質指標 | [arXiv:2310.11440](https://arxiv.org/abs/2310.11440) |
| MT-Bench / Chatbot Arena | 透過成對人類 + LLM 評判評估 LLM 輸出品質 | [arXiv:2306.05685](https://arxiv.org/abs/2306.05685) |

### 生成式影片模型（工具存取 — 2026 年市場）

| 模型 | 提供商 | 主要能力 | 存取 |
|---|---|---|---|
| Sora 2 / Sora 2 Pro | OpenAI | 同步對白 + 音效 + 背景音；電影／寫實／動漫風格；1080p 20 秒 | [OpenAI Videos API](https://developers.openai.com/api/docs/models/sora-2)（2026 年 9 月停用） |
| Veo 3.1 | Google DeepMind | 4K / 1080p / 720p、8 秒；原生音訊；可配置 16:9 與 9:16；多圖參考引導角色／物件 | [Gemini API](https://ai.google.dev/gemini-api/docs/video) / [Vertex AI](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/veo/3-1-generate) |
| Runway Gen-4 / Gen-4.5 / Aleph | Runway | ControlNet 引導、鏡頭路徑、風格鎖定、Layout Sketch；Aleph 用於影片轉影片編輯 | [Runway API](https://docs.dev.runwayml.com/) |
| Kling 3.0 | Kuaishou | 電影級動態擬真；物理準確；動態控制（參考影片）；原生音訊 | [Kling API (fal.ai)](https://fal.ai/models/fal-ai/kling-video) |

### 聲音與虛擬主播工具（2026）

| 工具 | 提供商 | 能力 |
|---|---|---|
| ElevenLabs v3 | ElevenLabs | 富表現力 TTS；即時／專業聲音克隆；對白模式（多人）；長篇用 Projects API；音效生成 | [文件](https://elevenlabs.io/docs) |
| HeyGen Avatar IV | HeyGen | 寫實 AI 虛擬主播；175+ 種語言嘴形對音；ElevenLabs 整合；個人化 API | [HeyGen](https://www.heygen.com) |
| Synthesia | Synthesia | 企業級 AI 虛擬主播大規模部署；SCORM 相容；品牌可控 | [Synthesia](https://www.synthesia.io) |
| Sync.so / Wav2Lip | 開源 + API | 嘴形對音覆蓋；音素—口型對齊 | [Sync.so](https://sync.so) |

### 基礎標準

| 標準 | 用途 | 狀態（2026） |
|---|---|---|
| C2PA（內容來源） | 為每個 AI 生成產物加密簽署 manifest；平台（YouTube、TikTok、Meta）自動標籤 | 歐盟 AI 法案實踐守則（2026 年 3 月）規定 C2PA 必須與浮水印結合。逾 2,300 個工具支援。[contentauthenticity.org](https://contentauthenticity.org/blog/the-state-of-content-authenticity-in-2026) |
| MCP（Model Context Protocol） | LLM ↔ 工具整合的開放標準；逾 2,300 個公開伺服器；Claude、VS Code、Cursor 等原生支援 | 由 Anthropic + OpenAI + Block 於 2025 年 12 月捐贈給 Agentic AI Foundation（Linux Foundation）。[modelcontextprotocol.io](https://modelcontextprotocol.io) |
| DSPy | 用於「程式設計而非 prompt 撰寫」的 LLM 框架；將宣告式管線編譯為優化過的提示詞／微調 | Stanford 維護；MIPRO 優化器；PromptOptimizerAgent 用其進行自動化提示詞改進。[github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy) |

---

*生成日期：2026 年 5 月。來源：[`ai_agent_video_production_workflow.md`](./ai_agent_video_production_workflow.md)。「工具存取」與「架構模式」欄位由代理職責推導，並對照 2026 年供應商文件與已發表研究驗證。*
