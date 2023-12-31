# Singing Voice Conversion

<!--Writerside adds this topic when you create a new documentation project.
You can use it as a sandbox to play with Writerside features, and remove it from the TOC when you don't need it anymore.
If you want to re-add it for your experiments, click + to create a new topic, choose Topic from Template, and select the 
"Starter" template.-->

## Results

### Evaluating training effectiveness
We may listen to the audio generated by the model and subjectively evaluate how similar it is to the original audio in the dataset. While this method is easy, it is highly subjective and cannot be quantitatively measured.


#### Audio 1 ("The detective followed the trail of clues left by the suspect."):
<tabs>
    <tab title="Original">
        <video src="orig_audio_0.mp4"/>
    </tab>
    <tab title="Step: 2400">
        <video src="gen_audio_0_2400.mp4"/>
    </tab>
    <tab title="Step: 20000"><video src="gen_audio_0_20000.mp4"/></tab>
    <tab title="Step: 44800"><video src="gen_audio_0_44800.mp4"/></tab>
</tabs>

Discussion: There is heavy artefacts in the generated file at step 2400, while the quality of the files generated at steps 20000 and 44800 were quite similar.


#### Audio 2 ("The violinist played the complicated piece with ease."):
<tabs>
    <tab title="Original">
        <video src="orig_audio_1.mp4"/>
    </tab>
    <tab title="Step: 2400">
        <video src="gen_audio_1_2400.mp4"/>
    </tab>
    <tab title="Step: 20000"><video src="gen_audio_1_20000.mp4"/></tab>
    <tab title="Step: 44800"><video src="gen_audio_1_44800.mp4"/></tab>
</tabs>
Discussion: There is heavy artefacts in the generated file at step 2400. For the files generated at steps 20000 and 44800, there were noticeable difference when the word "ease" is pronounced but the overall differences were subtle.

### Baseline Text-to-Speech Test
When the model is trained. We first use text-to-speech to evaluate the general quality of the model when reading a short text without singing:

Text-to-speech model: Azure `en-HK-SamNeural`

Model trained steps: 52000

<video src="result_tts_KL_auto_sovdiff.mp4"/>

Transcript:
```AI models, particularly those based on deep learning, can analyze large amounts of musical data and learn to generate new compositions in a variety of styles. These systems can create entirely new pieces of music, or they can be used to suggest ideas to human composers, such as melodies, chord progressions, or rhythms.```

### Inference Results

#### Audio 1:
<tabs>
    <tab title="Original">
        <video src="orig_aud2.mp4"/>
    </tab>
    <tab title="Inferred">
        <video src="gen_aud2.mp4"/>
    </tab>
</tabs>

#### Lyrics (Audio 1) {collapsible="true"}
of my life

She's got glitter for skin

My radiant beam in the night

I don't need no light to see you

Shine

It's your golden hour (oh)

You slow down time

In your golden hour (oh)

#### Discussion (Audio 1)
This is a pair of verse and chorus from the song JVKE – golden hour. The original vocals were high-pitched. To attain good results, it is required to set the output to -12 semitones (-1 octave). The end results were generally good. However, there were some artefacts that made the generated audio sound artificial and unnatural. There were also some problems with the pronunciation as some words were perceived as others. For example, “in your” in the original audio was perceived as “being your” in the output.

#### Audio 2:
<tabs>
    <tab title="Original">
        <video src="orig_aud1.mp4"/>
    </tab>
    <tab title="Inferred">
        <video src="gen_aud1.mp4"/>
    </tab>
</tabs>

#### Lyrics (Audio 2) {collapsible="true"}
It was just two lovers

Sittin' in the car, listening to Blonde

Fallin' for each other

Pink and orange skies, feelin' super childish

No Donald Glover

Missed call from my mother

Like, "Where you at tonight?" Got no alibi

I was all alone with the love

#### Discussion (Audio 2)
This is the rap verse of JVKE – golden hour. Since the pitch of the original audio was comparable to the pitch of audio from the training dataset, the results were generally good with the occasional artefacts.

#### Audio 3:
<tabs>
    <tab title="Original">
        <video src="orig_aud3.mp4"/>
    </tab>
    <tab title="Inferred">
        <video src="gen_aud3.mp4"/>
    </tab>
</tabs>

#### Lyrics (Audio 3) {collapsible="true"}
She'd take the world off my shoulders

If it was ever hard to move

She'd turn the rain to a rainbow

When I was living in the blue

Why then, if she is so perfect

Do I still wish that it was you?

Perfect don't mean that it's working

So what can I do? (Ooh)

When you're out of sight

In my mind

'Cause sometimes I look in her eyes

And that's where I find a glimpse of us

And I try to fall for her touch

But I'm thinking of the way it was

Said I'm fine and said I moved on

I'm only here passing time in her arms

Hoping I'll find

A glimpse of us

Tell me he savors your glory

Does he laugh the way I did?

Is this a part of your story?

One that I had never lived

Maybe one day you'll feel lonely

And in his eyes, you'll get a glimpse

Maybe you'll start slipping slowly

And find me again

When you're out of sight

In my mind

'Cause sometimes I look in her eyes

And that's where I find a glimpse of us

And I try to fall for her touch

But I'm thinking of the way it was

Said I'm fine and said I moved on

I'm only here passing time in her arms

Hoping I'll find

A glimpse of us

Ooh, ooh-ooh

Ooh, ooh-ooh

Ooh, ooh, ooh

'Cause sometimes I look in her eyes

And that's where I find a glimpse of us

And I try to fall for her touch

But I'm thinking of the way it was

Said I'm fine and said I moved on

I'm only here passing time in her arms

Hoping I'll find

A glimpse of us

#### Discussion (Audio 3)
This is the song Joji – Glimpse of Us. The original audio has heavy reverb, and the verse contains a high degree of backing vocal. The pitch of the original singer was also generally high. This represents a case where the input audio is unsatisfactory. The resulting synthesised audio was low quality, with many artefacts and many unintelligible words.

## Training the model locally
These steps assume you are on Windows and has an Nvidia GPU.

<procedure title="Downloading source" id="download">
    <step>
        <p>The source of so-vits-svc used for this project can be downloaded at <a href="https://github.com/svc-develop-team/so-vits-svc/tree/4.1-Stable">GitHub (svc-develop-team/so-vits-svc)</a></p>
        <img src="Screenshot_2023-12-04_193029.png" alt="GitHub" border-effect="line" thumbnail="true"/>
    </step>
    <step>
        <p>Download and unzip the archive.</p>
    </step>
</procedure>

<procedure title="Set up environment">
    <step>
        <p>A new Conda environment is recommended. Install Anaconda.</p>
    </step>
    <step>
        <p>In the root directory of the archive, open a conda prompt and create a new environment</p>
    </step>
    <step>
    <p>Run <code>conda activate [your environment name]</code></p>
</step>
<step><p>Run <code>pip install -r requirements-win.txt</code></p></step>
</procedure>

<procedure title="Prepare dataset" id="prepare_dataset">
    <step>Prepare at least 15 minutes of raw audio in <code>.wav</code> format. Pay attention to clarity and make sure there are no background noises or music</step>
    <step>Put the audio files into the <code>./dataset_raw/[speaker name]</code> directory and configure <code>./configs/config.json</code></step>
    <step>The structure of the files should be as follows:<code-block>
dataset_raw
└───[Speaker name]
    ├───1.wav
    ├───2.wav
    ├───...
    └───45698-4156-123(Vocals)_0.wav
</code-block></step>
</procedure>

<procedure title="Download pretrained models" id="download_pretrained_models">
    <step>Download the contentvec vocoder model <a href="https://ibm.box.com/s/z1wgl1stco8ffooyatzdwsqn2psd9lrr">checkpoint_best_legacy_500.pt</a> and store it at <code>./pretrain</code></step>
    <step>Download the pretrained generator model <a href="https://huggingface.co/Sucial/so-vits-svc4.1-pretrain_model/tree/main">G_0.pt</a> and store it at <code>./logs/44k</code></step>
    <step>Download the pretrained discriminator model <a href="https://huggingface.co/Sucial/so-vits-svc4.1-pretrain_model/tree/main">G_0.pt</a> and store it at <code>./logs/44k</code></step>
    <step>Download the pretrained diffusion model <a href="https://github.com/yxlllc/DDSP-SVC">provided by DDSP-SVC</a> and store it at <code>./logs/44k/diffusion</code></step>
</procedure>

<procedure title="Training" id="training">
    <step>Generate cluster with <code>python cluster/train_cluster.py --gpu</code></step>
    <step>Generate train indices with <code>python train_index.py -c configs/config.json</code></step>
    <step>Training of main <code>G</code> and <code>D</code> models can be started with <code>python train.py -c configs/config.json -m 44k</code></step>
    <step>(Optional) Training of main diffusion can be started with <code>python train_diff.py -c configs/diffusion.yaml</code></step>
</procedure>

<procedure title="Inference" id="inference">
    <step>Example function call: <code>python inference_main.py -m "logs/44k/G_XXXXX.pth" -c "configs/config.json" -n "source-audio.wav" -t 0 -s "Speaker Name"</code>, replace <code>XXXXX</code> with the saved step you wish to use for inference.</step>
</procedure>

### Available options

#### Mandatory parameters for `inference.py`:

-m, --model_path
: Path of generator model.

-c, --config_path
: Path of config file.

-n, --clean_names
: Name of input `wav` file stored inside the `./raw` directory.

-t, --trans
: Pitch shift (in semitones). 12 semitones is an octave.

-s, --spk_list
: Name of the speaker



[//]: # (## Write content)

[//]: # (%product% supports two types of markup: Markdown and XML.)

[//]: # (When you create a new help article, you can choose between two topic types, but this doesn't mean you have to stick to a single format.)

[//]: # (You can author content in Markdown and extend it with semantic attributes or inject entire XML elements.)

[//]: # ()
[//]: # (For example, this is how you inject a procedure:)

[//]: # ()
[//]: # (<procedure title="Inject a procedure" id="inject-a-procedure">)

[//]: # (    <step>)

[//]: # (        <p>Start typing <code>procedure</code> and select a procedure type from the completion suggestions:</p>)

[//]: # (        <img src="completion_procedure.png" alt="completion suggestions for procedure" border-effect="line"/>)

[//]: # (    </step>)

[//]: # (    <step>)

[//]: # (        <p>Press <shortcut>Tab</shortcut> or <shortcut>Enter</shortcut> to insert the markup.</p>)

[//]: # (    </step>)

[//]: # (</procedure>)

[//]: # ()
[//]: # (## Add interactive elements)

[//]: # ()
[//]: # (### Tabs)

[//]: # (To add switchable content, use tabs &#40;start typing `tabs` on a new line&#41;.)

[//]: # ()
[//]: # (<tabs>)

[//]: # (    <tab title="Markdown">)

[//]: # (        <code-block lang="plain text">![Alt Text]&#40;new_topic_options.png&#41;{ width=450 }</code-block>)

[//]: # (    </tab>)

[//]: # (    <tab title="Semantic markup">)

[//]: # (        <code-block lang="xml">)

[//]: # (            <![CDATA[<img src="new_topic_options.png" alt="Alt text" width="450px"/>]]></code-block>)

[//]: # (    </tab>)

[//]: # (</tabs>)

[//]: # ()
[//]: # (### Collapsible blocks)

[//]: # (Besides injecting entire XML elements, you can use attributes to configure the behavior of certain elements.)

[//]: # (For example, you can collapse a chapter that contains non-essential information like this:)

[//]: # ()
[//]: # (#### Supplementary info {collapsible="true"})

[//]: # (Content under such header will be collapsed by default, but you can modify the behavior by adding the following attribute:)

[//]: # (`default-state="expanded"`)

[//]: # ()
[//]: # (## Convert selection to XML)

[//]: # (If you need to extend an element with more functions, you can convert selected content from Markdown to semantic markup.)

[//]: # (For example, if you want to merge cells in a table, it's much easier to convert it to XML than do this in Markdown.)

[//]: # (Position the caret anywhere in the table and press <shortcut>Alt+Enter</shortcut>:)

[//]: # ()
[//]: # (<img src="convert_table_to_xml.png" alt="Convert table to XML" width="706" border-effect="line"/>)

[//]: # ()
[//]: # (## Feedback and support)

[//]: # (Please report any issues, usability improvements, or feature requests to our )

[//]: # (<a href="https://youtrack.jetbrains.com/newIssue?project=WRS">YouTrack project</a>)

[//]: # (&#40;you will need to register&#41;.)

[//]: # ()
[//]: # (You are welcome to join our)

[//]: # (<a href="https://jb.gg/WRS_Slack">public Slack workspace</a>.)

[//]: # (Before you do, please read our [Code of conduct]&#40;https://plugins.jetbrains.com/plugin/20158-writerside/docs/writerside-code-of-conduct.html&#41;.)

[//]: # (We assume that you’ve read and acknowledged it before joining.)

[//]: # ()
[//]: # (You can also always email us at [writerside@jetbrains.com]&#40;mailto:writerside@jetbrains.com&#41;.)

[//]: # ()
[//]: # (<seealso>)

[//]: # (    <category ref="wrs">)

[//]: # (        <a href="https://plugins.jetbrains.com/plugin/20158-writerside/docs/markup-reference.html">Markup reference</a>)

[//]: # (        <a href="https://plugins.jetbrains.com/plugin/20158-writerside/docs/manage-table-of-contents.html">Reorder topics in the TOC</a>)

[//]: # (        <a href="https://plugins.jetbrains.com/plugin/20158-writerside/docs/local-build.html">Build and publish</a>)

[//]: # (        <a href="https://plugins.jetbrains.com/plugin/20158-writerside/docs/configure-search.html">Configure Search</a>)

[//]: # (    </category>)

[//]: # (</seealso>)
