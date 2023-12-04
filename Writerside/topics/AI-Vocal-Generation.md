# AI Vocal Generation

<!--Writerside adds this topic when you create a new documentation project.
You can use it as a sandbox to play with Writerside features, and remove it from the TOC when you don't need it anymore.
If you want to re-add it for your experiments, click + to create a new topic, choose Topic from Template, and select the 
"Starter" template.-->

## Background information
### Software
The chosen software is Audimee AI Vocals.
<img src="Audimee.png" alt="Audimee" border-effect="line"/>

### Testing Demo
We would select two AI models to transfer a Mandarin studio demo song to test whether they can generate a high-quality song.
The original song demo is below.
<video src="original_demo.mp4"/>

### Lyrics
有些話想對你說 一直藏在我心中
噗通心跳的那一天 我對你的想念
如果世界會改變 時間會回到原點
決定做好我自己 重新的遇見你

晚上好 你的今天 現在 有什麼冒險
能不能 給我一分鐘 看著天空 你慢慢的放鬆

就發生在那一分鐘
你的笑容 一份衝動
點亮了我的星空 想對你說
就算你的以後 睡在他的雙肩
我依然在你的身邊 就算你看不見
為愛你存在 永不會改變

## Result
<tabs>
    <tab title="Model A">
        <video src="AudimeeAI_goodexample.mp4"/>
    </tab>
    <tab title="Model B">
        <video src="AudimeeAI_badexample.mp4"/>
    </tab>
</tabs>

### Discussion: 
Model A is specialized in genres such as Singer, Indie, and Pop, whereas Model B is tailored for Singer, EDM, and House styles. 
When subjected to identical audio inputs and pitch settings, a comparative analysis reveals that Model A outperforms Model B. 
Model A exhibits a decreased presence of electronic voice characteristics and anomalous sounds, while Model B's generated soundtracks are characterized by a higher level of noise. 
It is important to note that both Model A and Model B are not well-versed in Mandarin, leading to difficulties in accurately pronouncing the lyrics. 
The dissimilarities in the stylistic attributes of these AI models significantly contribute to the observed variations in performance outcomes.

### Findings:
To ensure the development of a proficient AI vocal generation model, several crucial factors need to be carefully considered. 
These factors encompass the quality of the input audio, the selection of specific AI artist models, the implementation of pitch shifting techniques, the intention of generating instrumental or non-instrumental sound, and the language utilized by the model. 
Attending to these factors collectively contributes to the attainment of a well-performed AI vocal generation model.