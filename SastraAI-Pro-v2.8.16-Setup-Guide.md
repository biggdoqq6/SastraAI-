# SastraAI Pro v2.8.16 — សេចក្ដីណែនាំដំឡើងសម្រាប់អ្នកទិញ

សម្រាប់ **Windows x64**។ សូមយក installer ពី [GitHub Releases ផ្លូវការ](https://github.com/biggdoqq6/SastraAI-/releases/tag/v2.8.16) ប៉ុណ្ណោះ។ អ្នកលក់ផ្ដល់ **Pro License Key** និង **Sastra VIP Access Key** ផ្សេងគ្នា។ កុំផ្ញើ key ទាំងនេះទៅអ្នកដទៃ។ ការបកប្រែតាម Cloud និងការបង្កើតសំឡេងខ្មែរត្រូវការអ៊ីនធឺណិត។

## 1. ដំឡើងកម្មវិធី

1. ទាញយក `SastraAI-Pro-Setup-2.8.16.exe` ពី release ផ្លូវការ។ បើចង់ផ្ទៀងផ្ទាត់ឯកសារ សូមប្រៀបធៀប SHA-256 ជាមួយ `SHA256SUMS-2.8.16.txt` ក្នុង release ដូចគ្នា។
2. បិទ SastraAI Pro ដែលកំពុងបើក រួចដំណើរការ installer។ អាចដំឡើងពីលើកំណែចាស់បាន; មិនចាំបាច់លុបគម្រោង ឬវីដេអូរបស់អ្នក។
3. Installer បច្ចុប្បន្នមិនទាន់មានហត្ថលេខាឌីជីថល Windows។ បើ Windows បង្ហាញ SmartScreen warning សូមផ្ទៀងផ្ទាត់ថាឯកសារមកពី release ផ្លូវការ និង checksum ត្រូវគ្នាមុនសម្រេចដំណើរការ។ បើគោលនយោបាយម៉ាស៊ីនរារាំង សូមទាក់ទងអ្នកលក់។

## 2. បើក Pro License

1. បើក Tool ហើយចុច **Trial** ខាងលើ។ ចុច **Copy ID** នៅ **Your Machine Hardware ID (HWID)** ហើយផ្ញើ ID នេះទៅអ្នកលក់។
2. យក Pro License Key ដែលអ្នកលក់បង្កើតសម្រាប់ម៉ាស៊ីននេះ ដាក់នៅ **Enter Activation License Key** រួចចុច **Activate License**។
3. ពេលបង្ហាញ **PRO Studio License Active** មុខងារ Pro ត្រូវបានបើក។ License នេះជាប់នឹងម៉ាស៊ីន និងរយៈពេលដែលអ្នកបានទិញ។

## 3. បើក Cloud AI សម្រាប់បកប្រែ

1. ចូល **Settings → AI & Translation** ហើយជ្រើស **SastraAI Neural Core (VIP Dedicated)**។
2. បញ្ចូល Sastra VIP Access Key ផ្ទាល់ខ្លួនក្នុង **Sastra VIP Access Key**។ រក្សា **Sastra Neural Server Endpoint** ជា `https://sastraai.online/v1` លុះត្រាតែអ្នកលក់ណែនាំផ្សេង។
3. ចុច **Test Connection** ហើយបន្ទាប់មក **Save Settings**។ បើឆ្លើយ HTTP 401/403 សូមពិនិត្យ key ឬទាក់ទងអ្នកលក់។ License មិនជំនួស VIP key ឬ quota របស់វាទេ។

## 4. ដំឡើង Transcript សម្រាប់រឿងចិន

1. ចូល **Settings → Speech-to-Text & Hardsub OCR** ហើយជ្រើស **SenseVoiceSmall**។
2. ជ្រើស **Processing Device: Auto (Recommended)** ឬ **GPU (NVIDIA CUDA)** បើមាន NVIDIA GPU សមស្រប។ ម៉ាស៊ីនគ្មាន NVIDIA អាចជ្រើស **CPU (INT8)**។
3. ជ្រើស **Audio Language: Chinese (Mandarin)**, **Speech Boundaries: Silero (Default)** និង **Speaker Comparison: Off (Default)**។
4. ចុច **Set Up Model** រង់ចាំទាញយក និងដំឡើង រួចចុច **Verify Setup** និង **Save Settings**។ GPU ត្រូវការការដំឡើង CUDA ដាច់ដោយឡែកដែល Tool នឹងរៀបចំក្នុងជំហាន Set Up Model។

## 5. មុខងារ AI បន្ថែម និងសំឡេង

- បើចង់ប្រើ **Faster-Whisper** ឬ **Vocal Cut (AI BGM)** ចូល **Settings → System & Performance** ហើយចុច **1-Click Install Local AI Engine**។ ការដំឡើងដំបូងត្រូវការអ៊ីនធឺណិត និងកន្លែងផ្ទុកគ្រប់គ្រាន់។ SenseVoiceSmall ប្រើ **Set Up Model** នៅជំហានទី 4 ដោយឡែក។
- ចូល **Settings → Voice & Audio Mixing** ហើយសាកសំឡេង **Male (Piseth)** ឬសំឡេងដែលចង់ប្រើ។ Khmer dubbing ប្រើសេវាសំឡេង Edge តាមអ៊ីនធឺណិត; មិនចាំបាច់ដំឡើង Python ប្រសិនបើ native voice client ដំណើរការ។
- មុខងារ **NVENC** ត្រូវការ NVIDIA GPU ដែលគាំទ្រ។ ម៉ាស៊ីន CPU អាចប្រើផ្លូវ render ធម្មតា។

## 6. សាកបកប្រែ និង Batch Videos

1. ចុច **Load Video** ហើយសាកវីដេអូខ្លីមួយជាមុន ដើម្បីពិនិត្យ Transcript, Khmer Translate, Subtitle និង Voice។ ពិនិត្យឈ្មោះតួអង្គ និងពេលវេលាសំឡេងមុនបង្ហោះ។
2. សម្រាប់រឿងច្រើនភាគ ចូល **Batch Videos → Add Drama Folder** ឬ **Add Video(s)**។ ជ្រើស **Mode**, **Voice**, **Audio** និង **Workers** តាមម៉ាស៊ីន។
3. ជ្រើស **Auto Retry: ON** សម្រាប់កំហុសបណ្ដាញបណ្ដោះអាសន្ន ឬ **OFF** បើចង់ពិនិត្យភាគដែលបរាជ័យមុនសាកឡើងវិញ រួចចុច **Start Batch Process**។ Tool នឹងពិនិត្យការភ្ជាប់ AI និងសេវាសំឡេងមុនដំណើរការ។
4. បើ update ពីកំណែចាស់ខណៈមានភាគខ្លះ Ready រួច សូមបើក Batch Videos វិញ ហើយចុច **Retry Incomplete** ម្តង។ កម្មវិធីរក្សាលទ្ធផល Ready; ពិនិត្យសារ **Review audio** លើសំឡេងសង្ស័យមុនបង្ហោះ។

## 7. Update កំណែបន្ទាប់

**សម្រាប់ការផ្លាស់ប្តូរ repository លើកនេះ:** អ្នកប្រើ v2.8.15 ឬចាស់ជាងនេះ ត្រូវទាញយក installer v2.8.16 ពី release ផ្លូវការនិងដំឡើងពីលើកំណែចាស់ម្តង។ បន្ទាប់មក **Settings → Software Updates → Check for Updates** នឹងប្រើ repository ថ្មីសម្រាប់កំណែបន្ទាប់។

បើជួបបញ្ហា សូមផ្ញើ **លេខកំណែកម្មវិធី**, **ជំហានដែលឈប់**, **សារ error**, និង **លេខភាគវីដេអូ** ទៅអ្នកលក់។ កុំផ្ញើ VIP key ឬ License Key ក្នុងរូបថតសាធារណៈ។
