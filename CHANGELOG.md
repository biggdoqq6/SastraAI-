# SastraAI Pro — Release Changelog & Version History

All notable changes, new features, and improvements to **SastraAI Pro** will be documented in this file.

---

## Unreleased

---

## [v2.8.16] — 2026-11-09

### Batch transcription recovery / ការសង្គ្រោះ Transcript ក្នុង Batch

- Recheck long music and sound-effect intervals with a stricter speech detector after focused and wide transcript repairs complete. Ambiguous audio remains marked for review; independently detected speech still blocks completion.
- If Cloud Audio fails and SenseVoiceSmall is already installed, retry that episode locally once. Authentication failures and cancelled jobs do not trigger the local fallback.
- Reproduced EP066, EP067, and EP070 from the affected 81-episode batch. All three completed transcription, Khmer translation, dubbing, and export. The full 81-episode movie was merged successfully.

**ខ្មែរ:** កែបញ្ហា 3 ភាគដែលជាប់នៅ Transcript ដោយសារ speech detector ច្រឡំសំឡេងភ្លេង/FX និង Cloud ផ្ញើ JSON ខុសទ្រង់ទ្រាយ។ កម្មវិធីផ្ទៀងផ្ទាត់ចន្លោះសំឡេងម្តងទៀត ហើយប្រើ SenseVoiceSmall ដែលបានដំឡើងរួចសម្រាប់សង្គ្រោះពេល Cloud Audio បរាជ័យ។ ចន្លោះសំឡេងមិនច្បាស់នៅតែមានសារ Review មុនផ្សាយ។

---

## [v2.8.15] — 2026-10-31

### Batch transcript recovery / ការកែ Transcript ក្នុង Batch

- Reproduced the repeated `Possible untranscribed speech remains near 11.1s` failure on the original 68-second episode 014. SenseVoiceSmall recognized the preceding and following lines, while Silero held a speech interval over music or sound after the preceding line.
- The coverage check now accepts a longer detector tail only when both focused and wide-context ASR recovery agree on the preceding words and no new dialogue appears in the gap. Minor Chinese erhua (`儿`) differences between decodes no longer force endless Auto Retry. Separate VAD pulses and genuinely recovered new words still block completion.
- Verified the complete episode transcript on both CPU and NVIDIA GPU: 20 source rows each. Uncertain audio remains marked for review before publication. The current translation API and dubbed export were not tested for this episode.

**ខ្មែរ:** កែបញ្ហាភាគ014 ដែល Auto Retry វិលជាប់ត្រង់ 11.1 វិនាទី ទោះពាក្យត្រូវបានស្គាល់រួច។ កម្មវិធីពិនិត្យលទ្ធផលស្គាល់សំឡេងពីរជុំ មុនប្តូរចុងសំឡេងសង្ស័យទៅជា Review warning។ បើមានសម្ដីថ្មីដែលខ្វះ វានៅតែរារាំងដើម្បីកុំឱ្យបាត់ពាក្យ។ បន្ទាប់ពី update សូមចុច **Retry Incomplete** ម្តងសម្រាប់ភាគដែលនៅសល់។

---

## [v2.8.14] — 2026-10-30

### Facebook publishing / ការរៀបចំបង្ហោះ Facebook

- Added an optional Facebook Publish Pack to Batch Videos. A successful run saves each completed episode video, a frame-based Khmer cover, a grounded Khmer title and caption in numbered episode folders before Auto-Merge can clean temporary clips. Pack failures keep individual outputs for retry.
- Clearing the last Batch Videos episode now removes the old Publish Pack and Auto-Merge notices from the workspace and saved configuration. The generated files remain in their output folder.

### Batch queue and recovery / ការគ្រប់គ្រងបញ្ជីភាគ

- Batch Videos **Add Video(s)** now appends to the existing queue instead of replacing it, preserving Ready/Merged episodes and their output paths. Folder, drag-and-drop, and sidebar Load Video additions use the same case-insensitive duplicate check.
- A removed episode no longer remains in the Studio preview. Clearing the final queue item persists as an intentionally empty queue, so older recovery data cannot restore it on relaunch. Batch Suite can remove Ready episodes and remembers when the user has cleared its queue.
- When Batch uses Vocal Cut, verify long Cloud Audio speech gaps against an isolated vocal stem before retrying the same intro repeatedly. Preserve a review warning for ambiguous source audio and keep genuinely uncovered vocal speech blocking completion.
- Keep Batch Auto Retry running when a voice-service HTTP 403 occurs in a different episode; only rejected translation access blocks the whole batch. This allows pending transcript recovery to resume after the first pass.
- Show a live retry countdown in both Batch Videos and Batch Suite so the cooldown is visibly active. The Auto Retry toggle is covered by an end-to-end UI test.

**ខ្មែរ:** Batch Videos អាចបង្កើត folder សម្រាប់បង្ហោះ Facebook ដោយមានវីដេអូ Cover ចំណងជើង និង caption ខ្មែរ តាមលេខភាគ។ ការបន្ថែមភាគថ្មីរក្សាភាគដែលបានបកប្រែរួច។ ពេលលុបភាគចេញ សារ Publish Pack ចាស់ និង Preview ចាស់នឹងបាត់ពី Tool; ឯកសារវីដេអូនៅលើកុំព្យូទ័រនៅដដែល។ Auto Retry បង្ហាញពេលរង់ចាំ និងបន្តភាគដែលអាចដំណើរការបាន។

---

## [v2.8.13] — 2026-10-29

### Customer setup and batch readiness / ការដំឡើង និង Batch
- The in-app **1-Click Install Local AI Engine** can install a compatible per-user Python 3.11 runtime when the customer does not have one, then set up and verify the optional Faster-Whisper and Demucs engines. The Python installer is fetched over HTTPS and checked against a pinned SHA-256 hash.
- Batch Videos and Batch Suite check cloud translation access before processing episodes. HTTP 401/403 and a missing direct API key show actionable Settings guidance before transcription starts. The check uses the HTTP status code even when a provider replaces the response text.
- Dubbed batch modes make a short Khmer voice availability check before processing. A hard HTTP 403 stops early with guidance; temporary voice or network failures continue through the existing Auto Retry flow. The temporary voice probe is removed after the check.
- Added a [Khmer customer setup guide](SastraAI-Pro-v2.8.13-Setup-Guide.md) for installation, license activation, VIP access, SenseVoiceSmall, optional local AI engines, voice testing, Batch Videos and updates.

### Distribution notes
- Windows x64 NSIS installer. Cloud translation and Khmer Edge voice need internet access and their respective service availability. Pro access and cloud quota are separate.
- The installer is not Authenticode signed. Customers should obtain it from the official release and verify its checksum. A Windows warning may still appear.

---

## [v2.8.12] — 2026-10-28

### Khmer voice generation / ការបង្កើតសំឡេងខ្មែរ
- Bundle `msedge-tts` 2.1.1, which uses the v2 `Sec-MS-GEC` WebSocket handshake required by the current Edge Read Aloud service. This repairs the HTTP 403 failure seen on customer installations that fell back to an outdated Python `edge-tts` package.
- Keep Python as an optional fallback. Customers no longer need to install or update Python to generate Khmer voice when the bundled native client can reach the speech service.
- Preserve the backend reason when Python is unavailable, remove authentication URLs from speech errors, and stop repeating a rejected HTTP 403 request four times per subtitle.

កំណែនេះកែការបង្កើតសំឡេងខ្មែរដែលបរាជ័យដោយ HTTP 403 លើម៉ាស៊ីនអ្នកប្រើ។ កម្មវិធីភ្ជាប់ TTS កំណែថ្មីក្នុង installer ដោយផ្ទាល់ ដូច្នេះមិនចាំបាច់ដំឡើង Python ដើម្បីបង្កើតសំឡេងទេ។ ពេលសេវាបដិសេធការភ្ជាប់ កម្មវិធីបង្ហាញសារច្បាស់ដោយមិនបង្ហាញ URL ដែលមាន token។

---

## [v2.8.11] — 2026-10-27

### Batch dubbing recovery / កែពេលសំឡេងក្នុង Batch
- Preserve a long speaker’s full source interval when a short interjection is nested inside it. Generate and mix both complete Khmer voice clips instead of shrinking the first speaker to an impossible 0.1-second slot.
- Reproduced the overlapping 45.21–49.11s dialogue and 45.34–45.58s interjection pattern from a real 46-line translation checkpoint. A real FFmpeg regression test verifies that all voice clips finish without cutting words. Truly impossible non-overlapping slots still stop for review.

នៅពេលតួអង្គម្នាក់និយាយឃ្លាវែង ហើយតួផ្សេងឆ្លៀតនិយាយឃ្លាខ្លី កម្មវិធីនឹងរក្សាពេលសំឡេងទាំងពីរតាមវីដេអូដើម។ Batch មិនចាំបាច់បកប្រែភាគដដែលឡើងវិញដោយសារចន្លោះ 0.1 វិនាទីក្លែងក្លាយនោះទេ។

### Update asset validation / ផ្ទៀងផ្ទាត់ឯកសារ Update
- `npm run dist` now checks the installer against `latest.yml` and validates that its blockmap covers the complete installer. The missing v2.8.9 blockmap was added to its published release so eligible upgrades can reuse unchanged blocks.

---

## [v2.8.10] — 2026-10-27

### Batch transcript completion / បញ្ចប់ Transcript ជាបាច់
- Recheck uncertain speech with a direct wide-context SenseVoiceSmall decode and a stricter speech detector. A sparse 2–3 second music or sound-effect interval becomes a visible review warning only after both checks; independently detected missing speech still blocks completion.
- Reproduced the 3.79–6.23 second false speech gap in episode 142. After the fix, the resumed 97-episode Batch advanced through Khmer translation and dubbing and produced the 51–147 full movie. Previously completed episodes were restored from the queue checkpoint and were not processed again.
- Keep transcript warnings for later human review before publication.

### Video effects and editing / កែពណ៌ និងទម្រង់វីដេអូ
- Provide 32 visual color presets, horizontal mirroring, left/right rotation, and 9:16 fill with positioning controls in the side editor while the video remains visible.
- Remove the bulky overlay preset list from the effects panel and retain the compact grouped controls.

### Release validation / ផ្ទៀងផ្ទាត់មុនចែកចាយ
- Build and test the Windows x64 application and package an installer with matching update metadata. The optional local speech models still require first-run setup on a customer's device; cloud translation still requires the configured provider access.

### Review uncertain audio without losing the episode
- Reproduced the 2:29 `第001集.mp4` failure at 21.3 seconds. The low-threshold speech detector marked ocean splash audio after a fully transcribed line as possible speech.
- Retry suspected gaps as before, then run a stronger speech check for any longer residual. Allow brief weak-only activity through with a visible review notice while still stopping on confident, sustained or excessive uncovered speech.
- Verified that the selected SastraAI Cloud endpoint transcribes the original 149-second audio into 45 subtitle rows, preserves review notices at uncertain audio points, and translates all 45 rows into a Khmer SRT.

### Speech coverage and cloud chunk repair
- Include audible laughter and other human vocal sounds in SastraAI Cloud Audio transcripts so speech detection does not report those moments as missing words.
- Cut long audio at independently detected quiet intervals near the target chunk length. This prevents conflicting transcriptions of the same line at a fixed chunk seam while keeping coverage checks and review notices.
- Reproduced the 81-second episode failure and verified the corrected cloud transcript on the same source audio.

### Respect the selected cloud provider
- Keep 9Router subtitle translation on the configured cloud endpoint, including retries and errors. Never switch to saved direct Google Gemini keys when that endpoint fails.
- Route Gemini Cloud Audio and the Local Whisper cloud backup through the 9Router endpoint and SastraAI Cloud access key when 9Router is selected. Request timed JSON with `input_audio` on `chat/completions`; the dedicated STT route returned text without subtitle timestamps. Preserve timing review notices.
- Show the selected audio provider and applicable access-key status in Settings. Preserve saved Google keys for explicitly selected direct Gemini mode.

ពេលជ្រើស 9Router ការបកប្រែ និង cloud backup របស់ Transcript ប្រើតែ endpoint និង SastraAI Cloud key ដែលបានកំណត់។ មិនប្ដូរទៅ Google API keys ដោយស្វ័យប្រវត្តិទៀតទេ។

### Reliable compatible-provider translation
- Accept a single complete JSON code fence from compatible gateways while still rejecting prose, unfinished responses and truncated streams. Keep native JSON schemas on API requests.
- Explain the exact required output fields in the prompt for gateways that ignore `response_format`. Reject schema definitions returned instead of subtitle data and include specific validation failures in repair requests.
- Reconcile out-of-range model indexes only when the complete original source text identifies exactly one requested line. Reject conflicting indexes, duplicate output IDs and ambiguous repeated dialogue.
- Retry only invalid lines with an accuracy-model cascade. Preserve the selected model for each initial batch, skip models on HTTP 503 cooldown, and keep the complete-translation and pure-Khmer checks.
- Remove API-key prefixes from cooldown logs. Make the workspace launcher resolve its own directory and launch without terminating unrelated Electron apps.

កែការអាន JSON ពី 9Router និងការណែនាំទម្រង់ចម្លើយ ដើម្បីបង្ការការជាប់ Translate នៅ batch ចុងក្រោយ។ សាក API ពិតលើរឿង 68.7 វិនាទី ដោយ Model ដែលបានជ្រើស បានបកប្រែគ្រប់ 31 ជួរ។

### Transcription recovery and timing review
- Fix whole-film failures caused by short VAD residuals and uncertain word timestamps. Use a 250 ms alignment tolerance while still detecting isolated short commands.
- Retry missing audio with two seconds of surrounding context. Remove the default Whisper instruction prompt that could be echoed as dialogue, and reject recovery text with low word confidence or high non-speech probability.
- Preserve valid transcripts with explicit review notices only when each remaining uncertain interval is shorter than one second and their combined duration is at most 3% of the clip. Empty transcripts, sustained gaps and excessive residual activity still fail visibly.
- Reject malformed repair output without discarding valid main results; avoid adding neighboring context twice. Keep transcript notices visible after Auto Pilot finishes.
- Compute pitch autocorrelation with FFT to preserve the existing classification while avoiding a CPU stall on each subtitle. Synchronize all packaged and embedded Whisper workers.

កែការជាប់ Error លើរឿងដែលមានចន្លោះសំឡេងខ្លីៗ ដោយពង្រីកបរិបទពេលចាប់សម្ដីឡើងវិញ និងរក្សា warning សម្រាប់ចំណុចមិនច្បាស់។ សម្ដីបាត់វែង ឬច្រើននៅតែត្រូវរារាំង។

### Moonshine Mandarin Tiny Streaming
- Add a compact Moonshine option under Speech-to-Text & Hardsub OCR, with isolated CPU runtime setup, offline Mandarin transcription, download progress, cancellation and disk-size reporting.
- Use the official pinned 0.1.5 native model catalog with resumable, checksum-verified downloads. The model files total 32,290,152 bytes; no PyTorch or CUDA is needed by Moonshine.
- Reuse the existing overlapping audio chunks and independent speech-coverage checks. Preserve finalized text and timings; fail on unresolved speech gaps, incomplete lines or malformed output, and retain a segment-timing review notice before dubbing.
- Share the optional ASR Python process runner and transcript parser with Qwen / Whisper. Keep existing engine choices and avoid cloud fallback for failed local Moonshine jobs.

បន្ថែម Moonshine Mandarin Tiny Streaming សម្រាប់ Transcript ភាសាចិន ដោយប្រើ CPU និងឯកសារម៉ូដែលប្រហែល 32.3MB។ កំណត់ពេល Subtitle តាមឃ្លាសម្ដី ហើយរក្សាការជូនដំណឹងឱ្យពិនិត្យមុន Dubbing។

### Qwen3-ASR local transcription
- Add Qwen3-ASR 0.6B and 1.7B to Speech-to-Text settings, with Qwen3-ForcedAligner-0.6B for word timing and optional speech segment timing.
- Use an isolated Python runtime, resumable model downloads, progress and cancellation. Release the ASR model before loading the aligner; Auto selects CPU when GPU memory is limited.
- Preserve original punctuation and every transcribed word when building subtitles. Reject incomplete alignment, empty detected speech and truncated generation; retain review notices for languages without word alignment.
- Save model, device, timing, language and vocabulary settings. Keep local Qwen failures visible instead of silently uploading audio to a cloud fallback.

បន្ថែម Qwen3-ASR ទាំង 0.6B និង 1.7B ជាមួយ ForcedAligner 0.6B។ អាចដំឡើង និងទាញយកតាម Settings ដោយប្រើ runtime ដាច់ពី Whisper។

### Transcription, translation and dialogue integrity
- Validate every requested subtitle index and original source line; repair missing or invalid results in batches and fail visibly if any spoken line remains incomplete.
- Reject mixed-script translations without deleting untranslated words. Share strict JSON handling across Gemini, 9Router and Hardsub OCR; reject truncated responses and failed OCR batches.
- Preserve Local Whisper Auto language detection and save/reload vocabulary prompts. Forward custom translation instructions to every provider and synchronize source-language controls.
- Persist evidence-backed character names, relationships and recent dialogue by series. Translate episodes in order while retaining concurrent dubbing/rendering; skip auto-merge when any selected episode fails.
- Transcribe cloud audio in overlapping short chunks, reconcile repeated words at chunk seams, and detect speech activity once per audio file. Retry uncovered speech; surface unresolved gaps and mark unavailable verification for review.
- Preserve complete source text when word alignment is incomplete, keep Windows CUDA DLL handles alive, and synchronize all packaged/embedded transcription scripts.
- Preserve action-only annotations as original audio, and report overlong synthesized dialogue instead of cutting off final words.
- Add `npm run test:translation` for provider, settings, context persistence, real FFmpeg and Python regression checks. No version bump, installer or release was created.

ការកែនេះបង្ការការបញ្ចប់ទាំងបកប្រែមិនគ្រប់ ការលុបពាក្យបរទេសដែលមិនទាន់បកប្រែ និងការកាត់ចុងសម្ដី។ បរិបទតួអង្គត្រូវបានរក្សាទុកតាមស៊េរី ហើយចន្លោះសំឡេងដែលនៅមិនអាចចាប់បានត្រូវជូនដំណឹងឱ្យពិនិត្យ។ ភាពត្រឹមត្រូវនៃសាច់រឿងនៅត្រូវផ្ទៀងផ្ទាត់ជាមួយប្រភពដើម។

---

## [v2.8.9] — 2026-10-23

### Vocal Cut audio and Batch re-processing / សំឡេង និងការដំណើរការភាគឡើងវិញ
- Corrected FFmpeg audio splitting for Khmer dubbing with isolated background music and auto-ducking.
- Added individual episode re-processing and range re-runs using the selected current settings.
- Derived full-movie names from Chinese drama folders and kept raw source videos out of dubbed-clip merges.

---

## [v2.8.8] — 2026-10-22

### Unified Local AI Engine (Faster-Whisper & Meta Demucs)
- **1-Click Local AI Installer:** Added automated installation for Faster-Whisper, Meta Demucs v4, SoundFile, and PyTorch (CUDA 12.1 for NVIDIA GPUs or CPU Multithreading).
- **Environment Diagnostic Dashboard:** Real-time environment checking for Python runtime, PyTorch engine, Faster-Whisper, Meta Demucs, and compute device target.
- **Python Setup Guidance:** Direct download link for official Python 3.11 64-bit installer with live environment refresh, guiding users to enable "Add python.exe to PATH".

### Safe GPU-to-CPU Fallback & Windows DLL Hardening
- **Windows DLL Directory Resolution:** Automatically locates and registers PyTorch and NVIDIA wheel DLL folders in Python 3.8+ on Windows to resolve missing cuBLAS/cuDNN library errors.
- **Resilient Model Initialization:** Faster-Whisper model loading now automatically catches CUDA driver or DLL errors and safely switches to CPU INT8 mode, eliminating crashes.
- **Built-in Wave Audio Fallback:** Added wave module fallback for acoustic pitch/gender classification when SoundFile is unavailable.

### FFmpeg Render Mute Bug Fix (Code 4294967274 / EINVAL)
- Fixed complex filtergraph generation in `burnSubtitles` and `dubVideo` when original audio volume is muted (`originalVol <= 0.01`), eliminating unconnected audio pad errors.

### TTS Character Voice Substring Collision Fix
- Resolved character voice mapping collision (`!p.includes('female')`), ensuring Elder Female and Child Female characters never receive male voices.

---

## [v2.8.1] — 2026-10-11

### Cloud Model Integration & Universal Routing
- Added full support for Anthropic Claude Sonnet 5.5, Opus 5.5, OpenAI GPT-6.1 Sol, and DeepSeek R1 & V3 reasoning models in SastraAI Cloud settings.
- Updated default SastraAI Cloud Gateway endpoint to `https://api.sastraai.online/v1` with automatic fallback and sub-second latency connection checks.
- Enhanced real-time quota telemetry and seamless multi-model fallback across Gemini, Claude, and OpenAI neural pools.

---

## [v2.7.7] — 2026-09-30

### Reliable episode merging / ការផ្គុំវីដេអូភាគឱ្យមើលបានរលូន
- Merge now checks codec headers, resolution, frame rate, time base, and audio layout before using lossless stream copy. FFmpeg could previously report success even when the resulting video had corrupted frames. / កម្មវិធីពិនិត្យ codec, ទំហំរូបភាព, frame rate, time base និងសំឡេង មុនប្រើ stream copy ព្រោះមុននេះ FFmpeg អាចបង្ហាញថាជោគជ័យ ប៉ុន្តែរូបភាពវីដេអូចេញខូច។
- Incompatible episodes are normalized in small groups to a consistent video and audio format, then joined into one movie. Short audio is padded to the video length. / ភាគដែលមានទម្រង់ខុសគ្នាត្រូវបានបម្លែងជាក្រុមតូចៗឱ្យមានរូបភាព និងសំឡេងទម្រង់តែមួយ រួចផ្គុំជាវីដេអូពេញ។ សំឡេងខ្លីត្រូវបានបំពេញឱ្យស្មើប្រវែងរូបភាព។
- The finished movie is checked for the expected duration before replacing an existing output. / ពិនិត្យប្រវែងវីដេអូដែលផ្គុំរួច មុនជំនួសឯកសារចេញចាស់។

### Batch Queue / ជួរវីដេអូច្រើនភាគ
- Auto-Merge starts once after completed episodes are collected and displays a failure message when needed. The manual Merge Episodes action uses the same reliable engine. / Auto-Merge ចាប់ផ្តើមតែម្តងក្រោយប្រមូលភាគដែលរួច ហើយបង្ហាញសារកំហុសប្រសិនបើបរាជ័យ។ Merge Episodes ដោយដៃក៏ប្រើម៉ាស៊ីនផ្គុំដូចគ្នា។

### Version and updates / កំណែ និងការអាប់ដេត
- Synchronized app version and release notes to `2.7.7` and packaged the installer, blockmap, and `latest.yml` together for auto-update. / ធ្វើសមកាលកម្មកំណែ និង release notes ទៅ `2.7.7` ព្រមទាំងឯកសារទាំងបីសម្រាប់ Auto-Update។

---

## [v2.7.6] — 2026-09-30

### Batch dubbing voices / សំឡេងបញ្ចូលសម្រាប់វីដេអូច្រើនភាគ
- Batch Episode Queue now offers only the natural Khmer voices Piseth and Sreymom. The nine drama profiles are no longer selectable in Batch Videos. / Batch Episode Queue មានជម្រើសតែសំឡេងធម្មតា Piseth និង Sreymom ហើយលែងមានជម្រើស drama profiles ទាំង ៩ ក្នុង Batch Videos។
- Dual Voice automatically maps detected male and female characters to Piseth and Sreymom. Existing character assignments still determine the matching gender, without applying the old profile pitch or rate changes. / Dual Voice ជ្រើស Piseth សម្រាប់តួប្រុស និង Sreymom សម្រាប់តួស្រីដោយស្វ័យប្រវត្តិ ដោយរក្សាការកំណត់ភេទតួដែលមានស្រាប់ ហើយមិនប្រើការប្រែ pitch ឬ rate តាម profile ចាស់។
- Single Voice now lets you choose either Piseth or Sreymom for the entire batch. Both dubbed video output modes use the same voice selection. / Single Voice អាចជ្រើស Piseth ឬ Sreymom សម្រាប់វីដេអូទាំងមូល ហើយទម្រង់នាំចេញវីដេអូមានសំឡេងទាំងពីរប្រើការកំណត់ដូចគ្នា។

### Version and updates / កំណែ និងការអាប់ដេត
- Synchronized app version and release notes to `2.7.6` and packaged the Windows installer, blockmap, and `latest.yml` together for auto-update. / ធ្វើសមកាលកម្មកំណែកម្មវិធី និង release notes ទៅ `2.7.6` ព្រមទាំងឯកសារទាំងបីសម្រាប់ Auto-Update។

---

## [v2.7.5] — 2026-09-30

### Voice timing and synthesis / ការកំណត់ពេល និងបង្កើតសំឡេង
- Dubbing can use natural silence between speakers to fit speech without cutting off short subtitle slots. Subtitle end times follow the synthesized speech duration. / សំឡេងបញ្ចូលអាចប្រើចន្លោះស្ងាត់រវាងតួអង្គ ហើយពេលបញ្ចប់ subtitle ត្រូវតាមប្រវែងសំឡេងនិយាយពិត។
- Edge-TTS rate adjustment and pitch-preserving FFmpeg `atempo` reduce synthesis failures on dense dialogue, with a short fade at clip edges. / ការសម្រួលល្បឿន Edge-TTS និង FFmpeg `atempo` កាត់បន្ថយកំហុសបង្កើតសំឡេង ហើយបន្ថែម fade ខ្លីនៅចុងសំឡេង។

### Export and timeline / ការនាំចេញ និង Timeline
- Corrected FFmpeg audio stream indexes and limited exported video duration to the source length. / កែលេខ audio stream របស់ FFmpeg និងកំណត់រយៈពេលវីដេអូចេញតាមវីដេអូដើម។
- Added out-of-bound subtitle detection, a `Trim Past Video` action, and a reset confirmation when loading a new video. / បន្ថែមការសម្គាល់ subtitle ហួសវីដេអូ ប៊ូតុង `Trim Past Video` និងការសួរបញ្ជាក់ពេលបើកវីដេអូថ្មី។

---

## [v2.7.4] — 2026-09-30

### Dense subtitle voice timing / ការសម្រួលសំឡេងឃ្លាវែង
- Long speech lines now retry Edge-TTS at an adaptive speaking rate before pitch-preserving FFmpeg tempo fitting. Tempo stages remain below 2x each, and lines that still cannot fit report both generated and available durations. / ឃ្លាវែងសាកល្បងបង្កើតសំឡេងក្នុងល្បឿនសមស្រប មុន FFmpeg បង្រួមបន្ថែម ហើយបង្ហាញរយៈពេលពិតបើនៅតែមិនអាចដាក់បាន។
- Translation batches include each subtitle's duration so Gemini can prefer concise Khmer dialogue that fits its time slot. / ផ្តល់រយៈពេល subtitle ទៅ Gemini ដើម្បីជួយបកប្រែឱ្យខ្លីសមពេល។

---

## [v2.7.3] — 2026-09-30

### Speaker and voice assignment / ការជ្រើសសំឡេងតួអង្គ
- Translation batches can include the matching audio excerpt so Gemini can classify the person speaking from the voice, with a text-only fallback if audio is unavailable. / បន្ថែមឈុតសំឡេងស្របនឹង subtitle ទៅក្នុងការបកប្រែ ដើម្បីជួយសម្គាល់អ្នកនិយាយ និងមានផ្លូវបម្រុងប្រើអត្ថបទ។
- Unknown gender no longer inherits the previous, potentially different character's female voice. Named speakers keep a consistent profile across batches. / ភេទមិនច្បាស់មិនយកសំឡេងតួមុនដោយស្វ័យប្រវត្តិ ហើយតួដែលមានឈ្មោះរក្សាសំឡេងឱ្យជាប់លាប់។
- Character Casting overrides stale per-row voice IDs in both Generate Audio paths. / ការជ្រើសសំឡេងតួដោយអ្នកប្រើប្រាស់មានអាទិភាពលើលេខ voice ចាស់ក្នុងជួរ subtitle។

### Workspace and export flow / ផ្ទាំងការងារ និងការនាំចេញ
- Removed repeated main-workspace shortcuts while keeping AI Translate in the header, voice removal and dubbing in Workspace Tools, and overlay controls beside the video preview. / កាត់បន្ថយប៊ូតុងស្ទួននៅផ្ទាំងធំ។
- Timeline's quick action now states that it generates audio for all translated subtitles. / ប៊ូតុង Timeline បង្ហាញច្បាស់ថាបង្កើតសំឡេងសម្រាប់ subtitle ទាំងអស់។
- Dubbing Studio opens the shared Export Center for rendering, and Batch Queue applies saved character voice casting through the shared voice-selection logic. / ការនាំចេញរួមនៅ Export Center ហើយ Batch Queue ប្រើសំឡេងតួដែលបានកំណត់។

---

## [v2.7.2] — 2026-09-30

### Reliable voice generation / ការបង្កើតសំឡេងឱ្យពេញលេញ
- Retries individual Edge-TTS failures up to three times and validates every generated clip. If any dialogue clip still fails, generation stops and reports its subtitle number instead of returning a track with silent gaps. / សាកល្បងបង្កើតសំឡេងឡើងវិញរហូតដល់បីដង ហើយបង្ហាញលេខ subtitle ដែលបរាជ័យ ជំនួសការបង្កើត track ដែលមានចន្លោះស្ងាត់។
- Identifies dialogue rows that have source text but no Khmer translation before voice generation. / បង្ហាញជួរដែលមានអត្ថបទដើម ប៉ុន្តែមិនទាន់មានអត្ថបទខ្មែរ។
- Fits the full spoken line into its subtitle time slot without cutting off its final words. Lines that cannot fit now report the row requiring shorter text or longer timing. / កុំកាត់ចុងឃ្លាសំឡេងដោយស្ងាត់ៗ ហើយប្រាប់លេខជួរដែលត្រូវកែអត្ថបទ ឬពេលវេលា។

### Drama dialogue and feedback / សន្ទនារឿងភាគ និងសារកំហុស
- Preserves spoken inner monologue inside `(...)` and `（...）` while skipping stage direction labels and songs. / រក្សាឃ្លានិយាយក្នុងវង់ក្រចក ដោយរំលងតែស្លាកសកម្មភាព និងចម្រៀង។
- Shows synthesis failures clearly in the dubbing studio. / បង្ហាញកំហុសបង្កើតសំឡេងឱ្យងាយឃើញក្នុងផ្ទាំង Dubbing។

---

## [v2.7.1] — 2026-09-30

### Export reliability / ស្ថិរភាពនាំចេញវីដេអូ
- Fixed FFmpeg filter graph audio stream indexes for dubbing, background music, green screen, and watermark inputs. Input indexes now remain integers, preventing render failure `-22` (`AVERROR(EINVAL)`). / កែលេខសម្គាល់ audio stream ឱ្យជាចំនួនគត់ ដើម្បីទប់ស្កាត់ការបរាជ័យពេល render។
- Detects whether the source video has an audio stream before mapping or mixing it. / ពិនិត្យថាវីដេអូដើមមានសំឡេងឬអត់ មុនពេលភ្ជាប់ និងលាយសំឡេង។
- Limits output duration to the source video to stop dubbed audio or music from extending the export. / កំណត់រយៈពេលវីដេអូចេញតាមវីដេអូដើម ដើម្បីកុំឱ្យសំឡេងរត់ហួស។

### Subtitle timing / ពេលវេលាចំណងជើងរង
- Loading a new video now asks whether to clear subtitles from the previous video. / ពេលបើកវីដេអូថ្មី កម្មវិធីសួរថាតើត្រូវលុប subtitle ចាស់ឬទេ។
- Subtitle rows starting beyond the video end show a `Past Video` badge, and `Trim Past Video` removes them in one click. / ជួរ subtitle ដែលចាប់ផ្តើមហួសចុងវីដេអូមានសញ្ញា `Past Video` ហើយអាចលុបដោយប៊ូតុង `Trim Past Video`។

### Version and updates / កំណែ និងការអាប់ដេត
- Synchronized the app version and in-app release notes to `2.7.1`. The Windows installer, blockmap, and `latest.yml` are published together for auto-update. / ធ្វើសមកាលកម្មលេខកំណែ និងកំណត់ហេតុអាប់ដេតក្នុងកម្មវិធី ហើយបោះពុម្ពឯកសារទាំងបីសម្រាប់ Auto-Update។

---

## [v2.6.9] — 2026-09-28

### 🌟 កំណែអាប់ដេតថ្មី និងមុខងារពិសេសៗ (What's New in v2.6.9)
- **ជួសជុលម៉ាស៊ីនបកប្រែ & ការពារការចេញអក្សរចិន (Critical Translation Engine Restoration & Language Shield):**
  - **Restored `gemini-2.5-flash` in Candidate Models:** បញ្ចូលម៉ូដែលល្បឿនលឿន `gemini-2.5-flash` ទៅក្នុងបញ្ជី Candidate Models ជាអាទិភាពដំបូង ដែលឆ្លើយតបរហ័សត្រឹមតែ ~1s លើ API Keys ដែលដំណើរការ រួមជាមួយម៉ូដែលបម្រុង `gemini-3.6-flash`, `gemini-3.5-flash-lite`, និង `gemini-3-flash-preview`។
  - **Zero Chinese Fallback Leakage:** ដោះស្រាយបញ្ហាធ្លាក់ចេញអក្សរចិនដើម (Raw Chinese) ចូលទៅក្នុងប្រអប់ចំណងជើងរងភាសាខ្មែរ ដោយដាក់លក្ខខណ្ឌតឹងរ៉ឹងត្រួតពិនិត្យអក្សរខ្មែរ Unicode (`/[\u1780-\u17FF]/`) — ដាច់ខាតមិនអនុញ្ញាតឱ្យបង្ហាញអក្សរចិនជំនួសភាសាខ្មែរឡើយ។
  - **Full 12+ Key Pool Traversal:** ពង្រីកការរត់តេស្ត API Keys រហូតដល់អស់គ្រប់ Key ទាំងអស់ក្នុង Key Vault (`maxBatchAttempts = totalKeys`) លុបចោលការកំណត់ចាស់ត្រឹមតែ 3 ដង ដែលជាហេតុធ្វើឱ្យជាប់គាំងមិនបានទៅដល់ Keys ដែលនៅមាន Quota។
  - **Resilient Request Timeouts:** ដំឡើងកម្រិត Timeout ដល់ ២៥ វិនាទី (Batch 10 segments) និង ១៥ វិនាទី (Single segment) ដើម្បីទប់ទល់ពេល Google Server មានចរាចរណ៍ទិន្នន័យកកស្ទះខ្ពស់។
  - **Scoped 404/Quota Error Isolation:** លុបចោលការ Ban ម៉ូដែលរយៈពេល ២៤ ម៉ោងជាសកល (`global 24h ban`) ដោយប្តូរមកកត់ត្រាកម្រិត Per-Key/Per-Project វិញ ជួយឱ្យ Key ផ្សេងទៀតដែលមានសិទ្ធិអាចដំណើរការបានជាប្រក្រតី។

- **ការវាស់ល្បឿន Latency ជាក់ស្តែង និងត្រឹមត្រូវ (Accurate Latency Measurement):**
  - **Direct Model Latency Reporting:** កែសម្រួលប្រព័ន្ធវាស់ Ping Latency ក្នុង Settings Modal ឱ្យបង្ហាញរយៈពេលឆ្លើយតបជាក់ស្តែងរបស់ម៉ូដែលដែលដំណើរការបានជោគជ័យ (ត្រឹម ~800ms - 1,200ms) ដោយមិនបូកសរុបរយៈពេលដែលបានចំណាយលើការសាកល្បងម៉ូដែលដែលបរាជ័យពីមុនៗ (ដែលធ្លាប់បង្ហាញរហូតដល់ 14,000ms) ឡើយ។
  - **Speed vs Queue Diagnostics:** បញ្ជាក់យ៉ាងច្បាស់លាស់រវាង Milliseconds (ms) តិច=លឿន និងស្ថានភាពតម្រង់ជួរលើ Server របស់ Google។

- **ប្រព័ន្ធស្តារ Key Vault ស្វ័យប្រវត្ត (Self-Healing Key Vault & Audit Button):**
  - **Auto-Reset Expired Banned Keys:** ប្រព័ន្ធស្វ័យប្រវត្តត្រួតពិនិត្យ និងដោះលែង (Unban) API Keys ដែលជាប់រវល់ ឬអស់ Quota បណ្តោះអាសន្ននៅពេលផុតកំណត់ Cooldown។
  - **One-Click Key Vault Reset & Audit:** ប៊ូតុង `Reset & Audit Key Pool` ក្នុងផ្ទាំង Settings ជួយសម្អាតស្ថានភាព Cooldown ទាំងអស់ និងធ្វើតេស្តសាកល្បង Model Cascade ឡើងវិញភ្លាមៗដោយចុចតែម្តង។

- **ការធ្វើបច្ចុប្បន្នភាពកំណែស្វ័យប្រវត្ត (Dynamic Release Notes & Version Sync):**
  - ធ្វើសមកាលកម្មទិន្នន័យ Version `2.6.9` ពេញលេញលើគ្រប់ផ្នែក (`package.json`, `versionChangelog.ts`, `main.ts`, `updaterService.ts`, `App.tsx`, `SettingsModal.tsx`)។
  - គាំទ្រការទាញយក និងបង្ហាញ Release Notes ភ្លាមៗពេលមានការអាប់ដេតពី GitHub Releases។

---

## [v2.6.8] — 2026-09-28

### 🌟 កំណែអាប់ដេតថ្មី និងមុខងារពិសេសៗ (What's New in v2.6.8)
- **ប្រព័ន្ធបង្ហាញ Release Notes ស្វ័យប្រវត្ត (Dynamic Version Release Notes Architecture):**
  - **Dynamic In-App Changelog:** លុបចោលបញ្ជីរឹង (Hardcoded static HTML) ក្នុង `SettingsModal.tsx` ដោយប្តូរមកប្រើប្រព័ន្ធ Centralized Changelog Registry (`src/data/versionChangelog.ts`) ដែលធ្វើបច្ចុប្បន្នភាព និងបង្ហាញចំណុចកែប្រែថ្មីៗស្របតាម Version កំពុងប្រើប្រាស់ពិតប្រាកដ។
  - **Incoming GitHub Release Notes Parser:** គាំទ្រការទាញយក និង Parse ចំណុចកែប្រែដោយស្វ័យប្រវត្តពី GitHub Releases (`updateInfo.releaseNotes`) ទាំងទម្រង់ Markdown និង HTML `<li>` tags មកបង្ហាញជា Bullet Points ស្អាតបាតភ្លាមៗ។
  - **Multi-Version History Selector:** បន្ថែម Dropdown រើសមើលប្រវត្តិ Version ចាស់ៗ (`v2.6.8`, `v2.6.7`, `v2.6.6`, `v2.6.5`) ព្រមទាំង Badge សម្គាល់ (`Active Installed Version`, `Incoming GitHub Release`, `Historical Release`)។
  - **Quick Update Action:** ប៊ូតុងរហ័ស `vX.X.X (New)` អនុញ្ញាតឱ្យចុចមើល Release Notes របស់កំណែថ្មីដែលទើបតែបានទាញយកដោយចុចតែម្តង។

- **ប្រព័ន្ធការពារ API Key មិនបាត់បង់ (Permanent Key Vault & Zero-Data-Loss Shield):**
  - **Synchronous Rehydration:** ការពារការបាត់បង់ API Key ដោយស្វ័យប្រវត្តិ នៅពេលបើក/បិទ Settings ឬបិទបើកកម្មវិធី តាមរយៈ synchronous localStorage rehydration និង `useEffect([isOpen, initialSettings])` re-sync។
  - **Permanent Storage Safeguard:** ការពារ Main Process មិនឱ្យ overwrite សោរ API Keys ដោយអារេទទទេ `[]` ឡើយ។
  - **Key Vault Status Badge & Inspector:** បង្ហាញផ្ទាំង Compact Key Vault Inspector ក្នុង Settings Modal មានសញ្ញា `12 Keys Locked`, បញ្ជីសោរ Masked (`AQ.Ab8RN6...`) និងស្ថិតិសុវត្ថិភាព។
  - **Multi-Model Latency Test:** មុខងារ Test Connection ឆ្លាតវៃ ដោយសាកល្បងម៉ូដែលដែលអ្នកប្រើប្រាស់បានរើសជាចម្បង (`gemini-3.6-flash`) និង Auto-Failover ទៅម៉ូដែលបន្ទាប់ពេលជួបបញ្ហា HTTP 503 ឬ 429។

- **ល្បឿននាំចេញវីដេអូកម្រិតខ្ពស់ និងការកែឈ្មោះវីដេអូ (Ultra-Fast NVENC Hardware Export & Fixed Video Naming):**
  - **Fast NVENC Export Optimization:** ដោះស្រាយបញ្ហា Export យូរដោយកាត់បន្ថយដំណាក់កាល Encode មិនចាំបាច់ និងប្រើប្រាស់ Hardware NVENC GPU Acceleration (`h264_nvenc`) ពេញទំហឹង ធ្វើឱ្យការនាំចេញវីដេអូរហ័សជាងមុន ៣x ទៅ ៤x និងគ្មានការគាំង UI (Zero Freeze)។
  - **Fixed Export Naming:** កែសម្រួលឈ្មោះវីដេអូពេល Export មិនឱ្យដាច់ ឬបាត់ឈ្មោះ ដោយទាញយកឈ្មោះវីដេអូដើម + ភាសាបកប្រែ + លេខភាគយ៉ាងច្បាស់លាស់។
  - **Real-Time Progress & ETA:** បង្ហាញភាគរយ % រត់ជាក់ស្តែង រួមជាមួយល្បឿន FPS, Speed Multiplier (ឧ. 2.4x) និងរយៈពេលដែលនៅសល់ (ETA)។

---

## [v2.6.7] — 2026-09-28

### 🌟 កំណែអាប់ដេតថ្មី និងមុខងារពិសេសៗ (What's New in v2.6.7)
- **កម្រងស្ទីល Button Effects ទាំង ១០ (10 Pro Cinematic Button Styles):**
  - បន្ថែមជម្រើសរចនាប័ទ្មប៊ូតុងស្ទូឌីយោទំនើបកម្រិត Pro ចំនួន ១០ ប្រភេទ ដែលដំណើរការ 60 FPS Hardware Rendered លើ Workspace Tools៖
    1. **Cyber Neon Glow (`neon` - [HOT]):** បន្ទាត់ឡាស៊ែរ Neon តាមពណ៌ Identity របស់ Tool នីមួយៗ (Video: ខៀវ, BGM: ផ្កាឈូក, TTS: មាស, AI: ក្រហម, Mute: ស្វាយ, Export: បៃតង, Style: ស្វាយខ្ចី, Vol: ស៊ីយ៉ាន) រួមជាមួយ Ambient Back-Glow និង Spark Pins។
    2. **Apple Vision Glass (`glass` - [SLEEK]):** ផ្ទៃកញ្ចក់ Frosted Glassmorphism ថ្លា + Hairline Specular Reflection + Soft 3D Elevation។
    3. **Broadcast 3D Deck (`deck` - [TACTILE]):** កុងសូល Hardware Deck (Blackmagic ATEM) មានជម្រៅ 3D ចុចផតចុះ 3px + LED Bar តាមពណ៌ Tool។
    4. **Conic Border Beam (`beam` - [ANIMATED]):** ខ្សែពន្លឺឡាស៊ែររត់វិលជុំវិញគែមរាងមូលនៃប៊ូតុង (Orbiting Conic Energy Beam) 60FPS យ៉ាងរលូន។
    5. **Matrix Tech Circuit (`circuit` - [CYBER]):** ជ្រុងប៊ូតុងមានសញ្ញាកូដ `[+]` `[#]` បែប Cyber Circuit + Scanline Pulse & Cyan Energy Glow។
    6. **Hollywood Cinema Gold (`gold` - [LUXURY]):** ផ្ទៃ Obsidian ពណ៌មាសទឹករលក 24K + Light Sheen Sweep (`anim-sheen`) រត់កាត់ផ្ទៃប៊ូតុងពេល Hover។
    7. **Synthwave 80s (`synthwave` - [RETRO]):** ពណ៌ស្វាយ-ស៊ីជម្ពូ Retro Outrun Gradient + Dual-tone Neon Backlight។
    8. **Swiss Studio Minimal (`minimal` - [CLEAN]):** ស្ទីល Minimal ស-ខ្មៅ ស្រឡះភ្នែកបំផុត មានពណ៌តែពេល Hover លើប៊ូតុង។
    9. **Holographic Prism (`holo` - [FUTURISTIC]):** ពន្លឺឥន្ទធនូពណ៌ pastel ចាំងផ្លាតប្តូរពណ៌តាមមុំពន្លឺ (`anim-holo` Chromatic Sheen)។
    10. **Deep Ocean Aqua (`aqua` - [GLOW]):** ពន្លឺពណ៌ទឹកសមុទ្រជ្រៅ Bioluminescent Cyan + Liquid Ripple Wave Effect។

- **កម្រងស្ទីលក្បាច់ខ្មែរ និងភាពយន្តទាំង ៦ (6 Khmer Cultural & Heritage Themes):**
  - **Cinema Cyber-Gold (`cyber_gold` - [KHMER]):** សម្ព័ន្ធមាសគូល័រភាពយន្តខ្មែរ & ABA Mobile ជាមួយកាំរស្មីមាស 24K Hairline Laser Sweep និង Watermark ស្លឹកពោធិ៍។
  - **Royal Palace Burgundy (`royal_aba` - [ROYAL]):** ពណ៌ក្រហមឈាមជ្រូករាជវាំង ឆើតឆាយ និងអភិជន។
  - **Angkor Wat Obsidian (`angkor_stone` - [HERITAGE]):** សំរិទ្ធថ្មប្រាសាទបុរាណអង្គរវត្ត ស្ងប់ស្ងាត់និងរឹងមាំ។
  - **Mekong Sacred Jade (`mekong_jade` - [SACRED]):** ត្បូងមរកតទន្លេមេគង្គ ត្រជាក់ភ្នែក និងស្រស់ស្រាយ។
  - **Lakhon Khol Theatrical (`lakhon_fire` - [DRAMA]):** ភ្លើងឆាកល្ខោនខោល ក្ដៅគគុកបែប 3D Tactile។
  - **Apsara Lotus Glass (`apsara_glass` - [MYSTIC]):** កញ្ចក់អ័ព្ទផ្កាឈូកទេពអប្សរា Frosted Glassmorphism។

- **រូបតំណាងក្បាច់ខ្មែរ Vector SVG សុទ្ធ ១០០% (Khmer Cultural Icons):**
  - បំពាក់ក្បាច់បុរាណខ្មែរគូរជា SVG ផ្ទាល់នៅលើប៊ូតុងទាំង ៨៖
    - **Load Video:** កំពូលប្រាង្គប្រាសាទអង្គរ (`AngkorSpire`)
    - **Load BGM:** ចាប៉ីដងវែងខ្មែរ (`ChapeiDongVeng`)
    - **Load A1 Audio:** ស័ង្ខទិព្វរាជវាំង (`RoyalConch`)
    - **Remove Voice:** ព្រះហស្តមុទ្រាស្ងប់ស្ងាត់ (`SilenceMudra`)
    - **Mute Video:** កណ្ដឹង/គងសំរិទ្ធបុរាណ (`BronzeBell`)
    - **Export SRT:** សាស្ត្រាស្លឹករឹត (`SlekRith`)
    - **Subtitle Style:** ក្បាច់ភ្ញីផ្កាចន្ទន៍ (`KbachPkaChan`)
    - **BGM Track/Volume:** ឈិងចង្វាក់តន្ត្រីបុរាណ (`RhythmBell`)
  - ប៊ូតុង Toggle បិទ/បើកក្បាច់ខ្មែរ (`Khmer Icons: ON/OFF`) ក្នុង Settings Modal។

- **ផ្ទាំង Settings Modal & Live Simulation Preview:**
  - បន្ថែមផ្ទាំង **Live Simulation Mini Shell** បង្ហាញរូបរាងប៊ូតុងពិតៗ ៤ គ្រាប់ស្របតាម Style ដែលបានរើស។
  - បន្ថែម **Active Style Description Card** បង្ហាញលក្ខណៈសម្បត្តិលម្អិតរបស់ Style នីមួយៗ។
  - រៀបចំ Style Cards ទាំង ១៦ ជា ២ ក្រុមធំៗ (10 Pro Cinematic Styles + 6 Khmer Heritage Themes) យ៉ាងមានរបៀបរៀបរយ។
  - ប៊ូតុង Quick Cycle (`Sparkles` icon) នៅលើ Workspace Tools Header ចុចមួយឃ្លីកប្តូរ Style ភ្លាមៗ។

- **Navbar Visual Effects Layer (12 Pro Themes):**
  - បំពាក់ Navbar FX Layer ចំនួន ១២ ប្រភេទ (Aurora, Glass, Gold, Matrix, Nebula, Synthwave, Quantum, Tokyo, Equalizer, Wuxia, Titanium, Aqua) ជាមួយប៊ូតុង Quick Cycle លើ Header។

---

## [v2.6.6] — 2026-09-28

### 🌟 កំណែអាប់ដេតថ្មី និងមុខងារពិសេសៗ (What's New in v2.6.6)
- **មុខងារអក្សររត់បែប Dynamic Kinetic Subtitles & ASS Karaoke (CapCut & TikTok Style):**
  - បន្ថែមម៉ូដ Animation Subtitle ទំនើបកម្រិត Pro ចំនួន ៤ ប្រភេទ៖
    1. **None (Static):** បង្ហាញអក្សររត់ស្ងៀមបែបធម្មតា។
    2. **Karaoke Glow:** អក្សររត់រំលេចពណ៌ពន្លឺតាមពាក្យនិយាយ (Neon Sweep Fill) យ៉ាងស្រទន់ និងទាក់ទាញភ្នែក។
    3. **Word Pop:** អក្សរលោតបាស់ឡើងលើ (Scale Bounce Pop) ទៅតាមពាក្យដែលកំពុងនិយាយក្នុងវីដេអូ ពេញនិយមបំផុតលើ CapCut, Reels និង TikTok។
    4. **Color Pill:** រុំព័ទ្ធពាក្យដែលកំពុងនិយាយដោយផ្លាកពណ៌កម្រិតពណ៌ច្បាស់ (Contrast Pill Badge)។
  - **បច្ចេកវិទ្យាកាត់ពាក្យខ្មែរតាមធម្មជាតិ (Khmer Word Segmentation Engine):**
    - ប្រើប្រាស់ Chromium Native `Intl.Segmenter('km', { granularity: 'word' })` ដែលមានវចនានុក្រមភាសាខ្មែរច្បាស់លាស់ ១០០% ដោយមិនបាច់ពឹងផ្អែកលើ Python ឬបណ្ណាល័យក្រៅឡើយ។
    - គណនាប្រវែងនិងរយៈពេលនិយាយនៃពាក្យនីមួយៗ (Syllable-Weighted Duration Distribution) ឱ្យត្រូវស៊ីចង្វាក់នឹងល្បឿនមាត់និយាយពិតៗ។
  - **ការបង្ហាញចលនាផ្ទាល់កម្រិត 60FPS លើ Video Player (Butter-Smooth In-Player Animation):**
    - ដំណើរការតាមរយៈ `requestAnimationFrame` ក្នុងពេលកំពុង Play វីដេអូ ធានាថាពាក្យនីមួយៗលោត Highlight យ៉ាងរលូនគ្មានទាក់ (Zero Jitter)។
    - មានមុខងារ Live Preview Simulation ផ្ទាល់ក្នុងផ្ទាំង Subtitle Typography & Styling Modal ដែលដំណើរការចលនាក្នុងពេលកំពុងជ្រើសរើសស្ទីល។
  - **ការនាំចេញវីដេអូ Hardsub កម្រិតខ្ពស់តាម FFmpeg ASS Subtitles:**
    - បញ្ចូលកូដ ASS Karaoke Tag (`{\kf<duration>}` សម្រាប់ Karaoke Glow និង `{\k<duration>}` សម្រាប់ Word Pop/Pill) ដោយស្វ័យប្រវត្តក្នុង Dialogue Events។
    - កំណត់ `PrimaryColour` ជាពណ៌ Highlight និង `SecondaryColour` ជាពណ៌អក្សរដើម ធានាថាពេល Export វីដេអូរួច ចលនាអក្សររត់នឹងដុតជាប់លើវីដេអូយ៉ាងច្បាស់ និងត្រឹមត្រូវតាមស្ដង់ដារភាពយន្ត។
  - **ផ្ទាំងគ្រប់គ្រងពណ៌ Highlight សម្បូរបែប:**
    - ជម្រើសពណ៌ទាក់ទាញចំនួន ៦ (Amber Gold, Electric Cyan, Neon Emerald, Coral Pink, Ultra Violet, Vibrant Orange) រួមជាមួយ Color Picker អាចរើសពណ៌តាមចិត្ត។
  - **អនុលោមតាមច្បាប់ AGENTS.md ១០០%:** មិនប្រើ Emoji ដាច់ខាត (ប្រើតែ Lucide SVG Icons), ឈ្មោះប៊ូតុងទាំងអស់ជាភាសាអង់គ្លេស, និង Layout មានរបៀបរៀបរយសន្សំទំហំ (Zero-scroll, Compact Controls)។
- **មុខងារបង្កើតរូបភាព Cover និងចំណងជើងទាក់ទាញ (AI High-CTR Thumbnail & Title Generator):**
  - **Best Keyframe AI Scanner:** ស្កេនចាប់យករូបភាពប្លង់វីដេអូដែលមានកម្រិតអារម្មណ៍ខ្ពស់បំផុត (Climax scene, action, shock, emotional tears) ឬចុចចាប់យករូបភាពពី Player បច្ចុប្បន្នភ្លាមៗតាមរយៈ Fast FFmpeg Seeking (<140ms)។
  - **Auto Poster Typography & Canvas Designer:**
    - រចនា Poster/Cover ស្វ័យប្រវត្តកម្រិតភាពយន្ត គាំទ្រ Aspect Ratio ចំនួន ៣ (`16:9` សម្រាប់ YouTube/Facebook, `9:16` សម្រាប់ TikTok/Reels, `1:1` សម្រាប់ Square)។
    - គាំទ្រពុម្ពអក្សរខ្មែរកម្រិតភាពយន្ត (Khmer Cinema Fonts: `Moul`, `Bokor`, `Battambang`, `Kantumruy Pro`, `Siemreap`) ជាមួយមុខងារ 3D Text Stroke និង Cinematic Vignette Overlay។
    - បន្ទះស្លាក Drama Badges ដែលមាន CTR ខ្ពស់បំផុត (ដូចជា "ភាគបញ្ចប់", "ការសងសឹក", "លាតត្រដាងការពិត", "អាថ៌កំបាំង")។
    - ជម្រើសពណ៌ភាពយន្តចំនួន ៤ (Cinema Gold, Crimson Fire, Electric Cyan, Studio White) និងប៊ូតុង Copy Image to Clipboard & Save PNG។
  - **Gemini Viral Title Generator:**
    - ប្រើប្រាស់ Gemini Structured Output (`application/json`) ដើម្បីបង្កើតចំណងជើង Viral ចំនួន ៥ ប្រភេទផ្សេងគ្នា (Shock & Reveal, Action & Revenge, Emotional Heartbreak, Curiosity Gap, Short & Punchy) ស្របតាមសាច់រឿងជាក់ស្តែង។
    - បង្កើត Trending Hashtags ស្វ័យប្រវត្ត និងមានប៊ូតុង Copy All ឬ Apply ផ្ទាល់ទៅកាន់ផ្ទាំង Poster Designer ដោយចុចតែម្តង (1-Click Insertion)។
  - **មុខងារបំប្លែង Poster ថ្មី និងបកប្រែចំណងជើងស្វ័យប្រវត្ត (AI Poster Remaker & Title Translator):**
    - **Gemini Vision OCR & Translation:** អានអក្សរចិនលើ Poster ដើមដោយស្វ័យប្រវត្ត រួចបកប្រែជាចំណងជើងរឿងភាគខ្មែរកម្រិតភាពយន្តដែលមាន CTR ខ្ពស់ (ឧ. *«កើតជាថ្មីជាស្ដេចខ្លា ប្អូនៗសុទ្ធតែកំពូលអ្នកខ្លាំងចាប់ជាតិ»*) រួមទាំងជម្រើសចំណងជើងបម្រុង ៤ ផ្សេងទៀត (Click to Apply)។
    - **Google Imagen 3 Clean Poster Generation:** វិភាគប្លង់ តួអង្គ សត្វខ្លា និងបរិយាកាសក្នុងរូបដើម រួចបង្កើតជា Prompt លម្អិតជាភាសាអង់គ្លេស ហើយ Generate រូបភាព Cover ថ្មីស្រឡាងស្អាតកម្រិត 8K គ្មានជាប់អក្សរចិន ឬ Watermark ឡើយ។
    - **Dual Image Switcher:** ផ្ទាំងប្តូររវាងរូបភាព Cover ថ្មីដែល Generate ដោយ AI (AI Clean Poster) និងរូបភាពដើម (Original Poster) ដោយចុចតែម្តង។
    - **Prompt Inspector & Variation Re-generator:** អាចកែសម្រួល Prompt តាមចិត្ត ហើយចុច Re-generate រូបភាពថ្មីបន្តបន្ទាប់បានភ្លាមៗ។

---

## [v2.6.5] — 2026-09-27

### 🌟 កំណែអាប់ដេតថ្មី និងការកែលម្អ (What's New in v2.6.5)
- **កំណត់សំឡេងនិយាយបែបធម្មតាសម្រាប់តួប្រុស និងតួស្រី (Natural Male & Female Speech - Pitch 0Hz):**
  - កែសម្រួល Pitch របស់សំឡេង **Default Female (Sreymom)** ពី `+10Hz` មកនៅត្រឹម `+0Hz` (Natural Speech) ស្មើនឹង Pitch ដើមពិតៗរបស់មនុស្សនិយាយ មិនធ្វើឱ្យសំឡេងស្រួយ/ស្រួចជ្រុលទៀតឡើយ។
  - កំណត់សំឡេង **Default Male (Piseth)** និង **Default Female (Sreymom)** ជាសំឡេងដើម (Natural Duo) ពេល Generate Audio ទាំងលើ Timeline Editor, Dubbing Modal និង Batch Queue។
  - លុបចោលការបង្ខំដំឡើង/ទម្លាក់ Pitch ដោយស្វ័យប្រវត្តតាមពាក្យអារម្មណ៍ (emotion heuristics ដូចជា cry/sad/angry) ដើម្បីធានាថារាល់ឃ្លាសន្ទនារឿងភាគ និយាយដោយសំនៀងធម្មជាតិ ១០០% ស្រទន់ ពិរោះ និងច្បាស់ល្អ។
  - បន្ថែមជម្រើស **Natural Duo (Male & Female)** នៅក្នុង Dubbing Modal ដែលអាចស្តាប់តេស្តសំឡេងធម្មជាតិទាំងពីរ និងកំណត់ភេទតួអង្គ (Male/Female) បានយ៉ាងរហ័ស។
- **ជួសជុលបញ្ហាអត់លឺសំឡេងលើ Voice Profile មួយចំនួន (Fixed Edge-TTS Negative Pitch/Rate Bug):**
  - ដោះស្រាយបញ្ហាធំមួយដែលធ្វើឱ្យបន្ទាត់ Subtitle ណាដែលជ្រើសរើស Voice Profile ជា **Elder Male (លោកតា/ព្រឹទ្ធាចារ្យ)**, **Elder Female (ម៉ែ/យាយ)**, **Demon/Monster (បិសាច)**, **Narrator (អ្នកនិទាន)** ឬតួអង្គដែលមាន Pitch និង Rate ជាសញ្ញាដក (`-25Hz`, `-5%`) មិនអាចបញ្ចេញសំឡេងបាន (ស្ងាត់/Silent) ដោយសារតែកម្មវិធី Python `argparse` ច្រឡំសញ្ញាដកថាជា option flag។
  - កែប្រែទម្រង់បញ្ជូន Command ទៅជា `--rate=...` និង `--pitch=...` រួមទាំងបន្ថែមប្រព័ន្ធ **Auto-Retry Resilience** ធានាថាគ្រប់បន្ទាត់ទាំងអស់ (ពិសេសបន្ទាត់ Elder Male ដូចក្នុងឈុតភាពយន្ត) នឹងបញ្ចេញសំឡេងបាន 100% យ៉ាងពិរោះ និងឥតបាត់បង់សំឡេងទៀតឡើយ។
- **ប្រព័ន្ធរកឃើញ Python Executable ឆ្លាតវៃសម្រាប់ TTS:**
  - ភ្ជាប់ប្រព័ន្ធស្វែងរក Python ស្វ័យប្រវត្តពី DemucsService មកកាន់ TTSService ដើម្បីធានាថាដំណើរការបំប្លែងសំឡេងអាន (Edge-TTS) ដំណើរការលើ Python Environment ត្រឹមត្រូវជានិច្ច គ្មានបញ្ហា Command Not Found។

---

## [v2.6.4] — 2026-09-27

### 🌟 កំណែអាប់ដេតថ្មី និងការកែលម្អ (What's New in v2.6.4)
- **ជួសជុល AI Demucs Vocal Separation ឱ្យដំណើរការ 100% លើ Production Build:**
  - ដោះស្រាយបញ្ហាដែលពីមុនពេលចែកចាយកម្មវិធីឱ្យអ្នកប្រើប្រាស់ ការបំបែកសំឡេង (Remove Vocal) តែងតែធ្លាក់ទៅប្រើ FFmpeg DSP Filter (ដែលធ្វើឱ្យបាត់បង់គុណភាពសំឡេង និងសល់សំឡេងនិយាយ) ដោយសារកម្មវិធីស្វែងរកឯកសារ script ក្រៅកញ្ចប់ installer។
  - ប្តូរមកដំណើរការ **Meta Demucs CLI (`python -m demucs.separate`)** ដោយផ្ទាល់ពី Python Environment រួមជាមួយការទាញយកសំឡេងពីវីដេអូតាមរយៈ **Bundled FFmpeg** ដោយស្វ័យប្រវត្ត។
  - ធានាថាដំណើរការបំបែកសំឡេងមនុស្ស និងតន្ត្រី (BGM / Vocals) ដំណើរការកម្រិត Studio Quality ពិតប្រាកដ 100% លើទាំង NVIDIA CUDA GPU និង CPU Multithreading។
- **ជួសជុលបញ្ហាអត់លឺសំឡេងលើ Voice Profile មួយចំនួន (Fixed Edge-TTS Negative Pitch/Rate Bug):**
  - ដោះស្រាយបញ្ហាធំមួយដែលធ្វើឱ្យបន្ទាត់ Subtitle ណាដែលជ្រើសរើស Voice Profile ដូចជា **Elder Male (លោកតា/ព្រឹទ្ធាចារ្យ)**, **Elder Female (ម៉ែ/យាយ)**, **Demon/Monster (បិសាច)**, **Narrator (អ្នកនិទាន)** ឬតួអង្គដែលមាន Pitch និង Rate ជាសញ្ញាដក (`-25Hz`, `-5%`) មិនអាចបញ្ចេញសំឡេងបាន (ស្ងាត់/Silent) ដោយសារតែកម្មវិធី Python `argparse` ច្រឡំសញ្ញាដកថាជា option flag។
  - កែប្រែទម្រង់បញ្ជូន Command ទៅជា `--rate=...` និង `--pitch=...` រួមទាំងបន្ថែមប្រព័ន្ធ **Auto-Retry Resilience** ធានាថាគ្រប់បន្ទាត់ទាំងអស់ (ពិសេសបន្ទាត់ Elder Male) នឹងបញ្ចេញសំឡេងបាន 100% យ៉ាងពិរោះ និងឥតបាត់បង់សំឡេងទៀតឡើយ។
- **ប្រព័ន្ធ Auto-Update ស្វ័យប្រវត្តបែបទំនើប (Silent 1-Click Update):**
  - កែប្រែប្រព័ន្ធ Update ទៅជា **One-Click Silent Install**។ នៅពេលទាញយកកំណែថ្មីរួចរាល់ កម្មវិធីនឹងដំឡើងជំនួសកំណែចាស់ដោយស្វ័យប្រវត្តក្នុងផ្ទៃក្រោយ (Background) ដោយមិនបាច់ចុច Next / Next / Install ញ៉ាំញ៉ាំដូចមុនទៀតឡើយ។
- **កែលម្អការបង្ហាញ Version និង Release Notes:**
  - ជួសជុលការបង្ហាញកូដ HTML លើផ្ទាំង Update Available Modal ឱ្យបង្ហាញជាអត្ថបទស្រឡះភ្នែក និងស្អាតត្រឹមត្រូវ។

---

## [v2.6.3] — 2026-09-27

### 🌟 កំណែអាប់ដេតថ្មី និងមុខងារពិសេសៗ (What's New in v2.6.3)
- **មុខងារដំឡើង Meta Demucs AI ដោយចុចតែម្តង (1-Click Installer):**
  - បន្ថែមផ្ទាំងគ្រប់គ្រង **Meta Demucs AI Neural Vocal Separation** នៅក្នុង **Settings ➔ System & Hardware Acceleration**។
  - សម្រាប់អ្នកប្រើប្រាស់ទូទៅ ឬ Laptop ថ្មីដែលមិនទាន់មាន Python/Demucs អាចដំឡើង AI Engine នេះបានដោយងាយស្រួលបំផុតដោយគ្រាន់តែចុចប៊ូតុង **"1-Click Install Demucs AI"** ផ្ទាល់ក្នុងកម្មវិធី។
- **ប្រព័ន្ធស្វែងរក និងកំណត់ GPU ឆ្លាតវៃ (Smart Hardware Detection):**
  - ពិនិត្យរកមើលក្រាហ្វិកកាត NVIDIA លើកុំព្យូទ័រដោយស្វ័យប្រវត្ត។
  - ប្រសិនបើមាន NVIDIA GPU: កម្មវិធីនឹងដំឡើង **PyTorch ជំនាន់ CUDA 12.1** ដោយស្វ័យប្រវត្ត ដើម្បីឱ្យដំណើរការបំបែកសំឡេងច្រៀង និងតន្ត្រីដំណើរការលើ GPU បានលឿនបំផុត (GPU Accelerated)។
  - ប្រសិនបើជាម៉ាស៊ីនទូទៅ (CPU): កម្មវិធីនឹងដំឡើង **PyTorch CPU Neural Engine** ដោយស្វ័យប្រវត្ត មិនធ្វើឱ្យ Error ឬគាំងម៉ាស៊ីនឡើយ។
- **ផ្ទាំង Terminal Console បង្ហាញដំណើរការដំឡើងផ្ទាល់ (Live Terminal Output):**
  - ផ្ទាំង Console ពណ៌ខ្មៅស្រឡះភ្នែក បង្ហាញព័ត៌មាននៃការទាញយក និងដំឡើងកញ្ចប់ Python Packages (pip install) ជាក់ស្តែងក្នុងពេលកំពុងដំណើរការ។
  - អាចចុច **View Console / Hide Console** និងមានប៊ូតុង **Cancel** ប្រសិនបើចង់ផ្អាកការដំឡើង។
- **ការភ្ជាប់ទំនាក់ទំនងរហ័សពីផ្ទាំង AI Voice Remover:**
  - នៅពេលបើកផ្ទាំង Voice Remover ប្រសិនបើម៉ាស៊ីនមិនទាន់មាន Demucs វានឹងបង្ហាញផ្ទាំងសាររំលឹក និងមានប៊ូតុង **[ Install in Settings ]** ដែលគ្រាន់តែចុចភ្លាម វានឹងនាំចូលទៅកាន់កន្លែងដំឡើងក្នុង Settings ភ្លាមៗ។
- **ជំនួយការទាញយក Python (Python Download Assistant):**
  - ប្រសិនបើកុំព្យូទ័រមិនទាន់មានដំឡើង Python 3 ទេ នឹងមានប៊ូតុង **"Download Python 3.11"** សម្រាប់បើកទៅកាន់គេហទំព័រផ្លូវការ Python ភ្លាមៗ។
- **ឯកសារជំនួយដំឡើងក្រៅកម្មវិធី (Standalone Batch Helper):**
  - មានភ្ជាប់មកជាមួយឯកសារ `tools/Install_Demucs_AI.bat` សម្រាប់ចុចដំឡើងដោយផ្ទាល់លើ Windows។

### 🛡️ សុវត្ថិភាព និងការរក្សាទិន្នន័យ (Security)
- **គ្មានការបែកធ្លាយ API Keys (Zero Key Leakage):**
  - បានផ្ទៀងផ្ទាត់យ៉ាងហ្មត់ចត់ថា រាល់ API Keys ផ្ទាល់ខ្លួនរបស់អ្នកអភិវឌ្ឍន៍មិនត្រូវបានបញ្ចូលទៅក្នុងកញ្ចប់កម្មវិធីដែលចែកចាយនោះឡើយ។

---

## [v2.6.2] — 2026-09-27

### 🌟 New Features & Enhancements
- **Appearance & Theme Studio:**
  - 5 Studio Themes: Dark Studio, Light Studio, OLED Pure Black, Cyber Studio, and Warm Sepia.
  - Dynamic Accent Colors: Indigo Pro, Amber Gold, Emerald Film, Rose Drama, and Cyan Neon.
  - UI Density controls (Comfortable / Compact) and Surface Finish options (Acrylic / Matte / OLED).
- **Admin Keygen GUI Tool:**
  - Standalone desktop key generator (`tools/keygen-gui.ts`) for licensing management.
  - Supports 30-Day, 90-Day, 1-Year, and Lifetime license activation codes.
- **Audio Auto-Ducking & Volume Normalization:**
  - Enhanced EBU R128 (-16 LUFS) broadcast-standard loudness leveling for drama dialogue.

---

## [v2.6.1] — 2026-09-27

### 🌟 New Features & Enhancements
- **Auto-Update Engine via GitHub Releases:**
  - Background update checking against `latest.yml`.
  - In-app `UpdateAvailableModal` with live download speed, progress bar, and restart installer trigger.
- **Settings Update Center:**
  - Added "Software Updates" tab in Settings to check version on demand.

---

## [v2.6.0] — 2026-09-26

### 🌟 Commercial Release Foundation
- **Offline RSA Hardware ID Licensing:**
  - Cryptographically signed `.lic` and activation code verification bound to CPU/Motherboard UUID.
- **Batch Processing & GPU Concurrency:**
  - Parallel worker pools supporting up to 4 concurrent episodes with NVIDIA NVENC video encoding.
- **Lossless Movie Merging:**
  - 2-5 second lossless episode concatenation via FFmpeg Concat Demuxer (`-c copy`).
