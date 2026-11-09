# SastraAI Pro v2.8.16 — Batch Speech Recovery

## ខ្មែរ

- កែបញ្ហាភាគដែលជាប់ `Transcribing` ព្រោះសំឡេងភ្លេង ឬ FX ត្រូវ speech detector ច្រឡំថាជាសម្ដី។ កម្មវិធីផ្ទៀងផ្ទាត់សំឡេងពីរជុំ និងពិនិត្យកម្រិតខ្លាំងម្តងទៀត មុនបន្តទៅ Translate។ ចន្លោះសង្ស័យនៅតែមានសារ **Review audio** សម្រាប់ពិនិត្យមុនផ្សាយ។
- បើ Cloud Audio ផ្ញើ Transcript ខុសទ្រង់ទ្រាយ ឬបរាជ័យ កម្មវិធីអាចប្រើ SenseVoiceSmall ដែលបានដំឡើងរួចសម្រាប់សង្គ្រោះភាគនោះ។ កំហុស key មិនត្រូវសាកម្តងទៀតតាមផ្លូវនេះទេ។
- បានសាកលើ EP066, EP067 និង EP070 ពី Batch 81 ភាគពិត៖ ភាគទាំងបីបានបញ្ចប់ Transcript, Khmer Translate, dubbing និង export; Full Movie 81 ភាគបាន merge ជោគជ័យ។

**ការផ្លាស់ប្តូរ repository:** កំណែចាស់ចង្អុលទៅ GitHub release URL ដែលលែងមាន។ អ្នកប្រើ v2.8.15 ឬចាស់ជាងនេះ ត្រូវទាញយក installer v2.8.16 ពី release នេះ និងដំឡើងពីលើកំណែចាស់ម្តង។ ចាប់ពី v2.8.16 ទៅ **Settings → Software Updates** នឹងប្រើ repository ថ្មី។ [សេចក្ដីណែនាំដំឡើង](https://github.com/biggdoqq6/SastraAI-/releases/download/v2.8.16/SastraAI-Pro-v2.8.16-Setup-Guide.md)

## English

- Resolve repeated Batch transcription retries caused by music and sound effects being detected as speech. Focused and wide repairs run before a stricter speech audit. Uncertain audio remains marked for review; independently detected dialogue still blocks an incomplete transcript.
- When Cloud Audio fails, an already installed SenseVoiceSmall engine can recover that episode locally. Rejected credentials and cancelled jobs do not trigger the fallback.
- Verified the affected EP066, EP067, and EP070 through transcription, Khmer translation, voice dubbing, and video export. The full 81-episode movie merged successfully.

**Update source migration:** Versions up to v2.8.15 point to a GitHub release URL that is no longer available. Install v2.8.16 once from this release; later in-app updates will use the new repository.

Windows x64 installer. Cloud translation and Khmer voice generation require their respective online services. SenseVoiceSmall fallback requires its optional model to be installed in the app. Review uncertain audio before publishing.

## Release assets

- `SastraAI-Pro-Setup-2.8.16.exe` — Windows installer
- `SastraAI-Pro-Setup-2.8.16.exe.blockmap` — differential update map
- `latest.yml` — update metadata; its SHA-512 must match the installer
- `SHA256SUMS-2.8.16.txt` — installer SHA-256 checksum
- `SastraAI-Pro-v2.8.16-Setup-Guide.md` — Khmer customer setup guide
