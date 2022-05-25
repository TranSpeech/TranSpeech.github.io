


{:.no_toc}
* toc
{:toc}


Direct speech-to-speech translation (S2ST) systems leverage recent progress in speech representation learning, where a sequence of discrete representations (units) derived in a self-supervised manner, are predicted from the model and passed to a vocoder for speech synthesis, still facing the following challenges: 1) Acoustic multimodality: the discrete units derived from speech with same content could be indeterministic due to the acoustic property (e.g., rhythm, pitch, and energy), which causes deterioration of translation accuracy; 2) high latency: current S2ST systems utilize autoregressive models which predict each unit conditioned on the sequence previously generated, failing to take full advantage of parallelism. In this work, we propose TranSpeech, a speech-to-speech translation model with bilateral perturbation. To alleviate the acoustic multimodal problem, we propose bilateral perturbation, which consists of the style normalization and information enhancement stages, to learn only the linguistic information from speech samples and generate more deterministic representations. With reduced multimodality, we step forward and become the first to establish a non-autoregressive S2ST technique, which repeatedly masks and predicts unit choices and produces high17 accuracy results in just a few cycles. Experimental results on three language pairs demonstrate the state-of-the-art results by up to 2.5 BLEU points over the best publicly-available textless S2ST baseline. Moreover, TranSpeech shows a significant improvement in inference latency, enabling speedup up to 21.4x than autoregressive technique.

Audio samples are available at <a href="https://TranSpeech.github.io/"><i>https://TranSpeech.github.io/</i></a>.

<br>

# Bilateral Perturbation

Utterances with the single-perturbed acoustic condition, remaining the linguistic content unchanged. 

RR: random resampling. F: a chain function $F = fs(pr(peq(x)))$ for random pitch shifting. 


<br>
<ruby>Text: really interesting work will finally be undertaken on that topicreally interesting work will finally be undertaken on that topic.</ruby>
<table>
	<thead>
		<tr>
			<th style="text-align: center">Original</th>
            <th style="text-align: center">Pitch Norm</th>
			<th style="text-align: center">Energy Norm</th>
			<th style="text-align: center">F</th>
            <th style="text-align: center">RR</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/1_original.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/1_pitch_norm.wav" type="audio/wav"></audio></td>
            <td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/1_energy_norm.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/1_F.wav" type="audio/wav"></audio></td>
            <td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/1_RR.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<ruby>Text: an inter ministerial committee on disability was held a few weeks back.</ruby>
<table>
	<thead>
		<tr>
			<th style="text-align: center">Original</th>
            <th style="text-align: center">Pitch Norm</th>
			<th style="text-align: center">Energy Norm</th>
			<th style="text-align: center">F</th>
            <th style="text-align: center">RR</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/2_original.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/2_pitch_norm.wav" type="audio/wav"></audio></td>
            <td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/2_energy_norm.wav" type="audio/wav"></audio></td>
			<td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/2_F.wav" type="audio/wav"></audio></td>
            <td style="text-align: center"><audio controls style="width: 150px;"><source src="wav_for_demo/BiP/2_RR.wav" type="audio/wav"></audio></td>
		</tr>
	</tbody>
</table>

<br/>

# Translation Results
DirectS2ST: Baseline model in `Direct speech-to-speech translation with discrete units.`

TextlessS2ST: Baseline model in `Textless speech-to-speech translation on real data.`

TranSpeech: TranSpeech with 5 mask-predict iterations.

## En-Es

<br>

<table>
        <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr>
        <tr>
            <th></th>
            <th>Source (English)</th>
            <th>Target (Spanish)</th>
            <th>DirectS2ST</th>
            <th>TextlessS2ST</th>
            <th>TranSpeech</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 1: </th>
        </tr> -->
        <tr>
            <th>Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/2_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/2_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_07/2_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_024/2_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/2_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> it can be found in algeria lebanon portugal and spain </td>
            <td> se encuentra en argelia líbano portugal y españa </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> se encuentra en argeria libanía portugal y españa </td>
            <td> se encuentra en argelia livana portugal y españa </td>
            <td> se encuentra en argelia líbano portugal y españa </td>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/4_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/4_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_07/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_024/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> afterwards they performed exhibitions in russia finland greece and poland </td>
            <td> posteriormente realizó exposiciones en rusia finlandia grecia y polonia </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> o durante realidades exposiciones en rusia filandia finlandia y polonia </td>
            <td> posteriormente realizaron exposiciones en rusia finlandia grecia y polonia </td>
            <td> posteriormente realizó exposiciones en rusia finlandia grecia y poloni </td>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 3: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/5_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/5_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_07/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_024/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Es/task_043/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> they are annual or perennial plants alpine and herbaceous </td>
            <td> son plantas anuales o perennes alpinas y herbáceas </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> son plantas anuales o perennes y herbáceas </td>
            <td> son plantas o plantas o perennes y rbáceas herbáceas </td>
            <td> son plantas anuales o perennes alpinas y herbáceas </td>
        </tr>
</table>

<br/>

## En-Fr

<br>

<table>
        <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr>
        <tr>
            <th></th>
            <th>Source (English)</th>
            <th>Target (French)</th>
            <th>DirectS2ST</th>
            <th>TextlessS2ST</th>
            <th>TranSpeech</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/1_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/1_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_07/1_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_024/1_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/1_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> the town includes several villages and hamlets </td>
            <td> la commune comprend plusieurs villages et hameaux </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> la commune comporte de nombreux villages et hameaux </td>
            <td> la commune comprend plusieurs villages et hameaux </td>
            <td> la commune comprend plusieurs villages et hameaux </td>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/3_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/3_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_07/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_024/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> the dolmen is classified as a national monument by the irish state </td>
            <td> le dolmen est classé comme monument national par l'état irlandais </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> le dolman est classé comme un monument national par l'état elandes </td>
            <td> le domaine est classé comme monument national par l'état ilandais </td>
            <td> le dolmen est classé comme monument national par l'état </td>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 3: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/4_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/4_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_07/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_024/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/En_Fr/task_043/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> what is the committee's opinion favorable opinion on this precision </td>
            <td> quel est l'avis de la commission avis favorable à cette précision </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> quel est l'avis de la commission avis favorable de cette précision </td>
            <td> quel est l'avis de la commission avis favorable à cette précision </td>
            <td> quel est l'avis de la commission avis favorable à cette précision </td>
        </tr>
</table>

<br>

## Fr-En

<br>

<table>
        <tr>
            <th></th>
            <th colspan="2">Ground truth</th>
            <th colspan="3">Predictions</th>
        </tr>
        <tr>
            <th></th>
            <th>Source (French)</th>
            <th>Target (English)</th>
            <th>DirectS2ST</th>
            <th>TextlessS2ST</th>
            <th>TranSpeech</th>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 1: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/5_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/5_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_07/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_024/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/5_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> un membre de la commission municipale du gouvernement provisoire </td>
            <td> a member of the municipal commission of the provisional government </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> amint solimin ici pal commission of the provision </td>
            <td> a member of the government commission the government takes place </td>
            <td> a member of the municipal commission of the provisional government </td>
        </tr>
        <tr> <th></th></tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 2: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/4_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/4_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_07/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_024/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/4_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> dans le nord de la france le terme correspondant est panne </td>
            <td> in the north of france the corresponding term is penne </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> in the north of france the corresponding term is north of france </td>
            <td> in the north of france the term corresponding is </td>
            <td> in the north of france the corresponding term is north of france </td>
        </tr>
        <!-- <tr>
            <th colspan="6" style="text-align:left">Sample 2: </th>
        </tr> -->
        <tr>
            <th>Sample 3: </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/3_source.wav"  type="audio/wav"></audio>
           </th>            
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/3_gt_translated.wav"          type="audio/wav"></audio>
           </th>
           <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_07/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_024/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
            <th>
                <audio controls style="width: 150px;"><source src="wav_for_demo/Fr_En/task_043/3_syn_translated.wav"          type="audio/wav"></audio>
           </th>
        </tr>
        <tr>
            <th> Reference: </th>
            <td> le château appartient à la famille noble de soirier </td>
            <td> the castle belongs to the noble de soirier familyx </td>
            <td> </td>
            <td> </td>
            <td> </td>
        </tr>
        <tr>
            <th> ASR: </th>
            <td> </td>
            <td> </td>
            <td> the castle belongs to the noble family of </td>
            <td> the castle belongs to the noble desire family </td>
            <td> the castle belongs to the noble desire family </td>
        </tr>
</table>
