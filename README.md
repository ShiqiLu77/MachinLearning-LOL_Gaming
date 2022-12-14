# 6105 Final Project: ๐ฎ LOL Match predict
Welcome to the summoner's rift!
![image](https://user-images.githubusercontent.com/113652536/206945150-36d73403-06cf-43b9-9527-7cdf16a29338.png)

## Contributors

Shiqi Lu, Jiawei Wang, Zeyu Liao

## You may want to know:

### File Tree:
```
Root:
โ  .DS_Store
โ  ChampionIdMapping.py	(Mapping Champions name into id)
โ  DecisionTree.ipynb		(Decision Tree model)
โ  DecisionTree2.ipynb														
โ  LogisticRegression.ipynb		(LogisticRegression model)
โ  MLP.ipynb										(MLP model)
โ  README.txt
โ  tmp2.ipynb
โ  ๆต่ฏๅณ็ญๆ ้ขๆต็ๆจกๆ้ตๅฎนๆๆ.ipynb
โ  
โโdataProcessingAlgorithms (Codes to convert raw data into featured data )
โ  โ  .DS_Store
โ  โ  ChampionNameMapping.py (Mapping Champions name into id)
โ  โ  GenerateInputDataForMLModel.py (Convert data into ml model acceptable input)
โ  โ  step1.MergeOriginCsvsToOneCsv.ipynb (Combined 87 CSV into 1 CSV )
โ  โ  step2.ChampionJsonToDF.ipynb (Read Json format champions values)
โ  โ  step3.1.DataProcessing-dropNanAndUselessColumns.ipynb (drop Nan And Useless Columns)
โ  โ  step3.2.DataProcessing-dropOutliers.ipynb (drop Outliers)
โ  โ  step4.SplitByTime.ipynb (Spilt data into three stages data pre stage, mid stage, and late stage)
โ  โ  step5.1.ChampionCounterScores.ipynb (Calculate counter score)
โ  โ  step5.2.ChampionWinRate.ipynb (Calculate win rate)
โ  โ  step5.4&5&6.ChampionControl&Attack&DefenseScore.ipynb (Calculate champion score)
โ  โ  step6.transformOriTraindataToSelectedFeatureData.ipynb (Convert data into ml model acceptable input)
โ  โ  step7.transformTestdataToSelectedFeatureData.ipynb
โ  โ  
โ  โโ__pycache__
โ          ChampionNameMapping.cpython-310.pyc
โ          ChampionNameMapping.cpython-39.pyc
โ          GenerateInputDataForMLModel.cpython-310.pyc
โ          GenerateInputDataForMLModel.cpython-39.pyc
โ          
โโdatasets (All datasets include original data and processed data)
โ  โ  .DS_Store
โ  โ  championCrossJoin.csv (original data after preprocess: drop NaN values, Time spilt etc.)
โ  โ  championId.csv
โ  โ  train_late.csv
โ  โ  train_mid.csv
โ  โ  train_pre.csv
โ  โ  val_late.csv
โ  โ  val_mid.csv
โ  โ  val_pre.csv
โ  โ  
โ  โโall_feature_data (processed data with all useful features )
โ  โ     
โ  โโcomparison_feature_data (processed data with compared useful features, eg. diff between two teams )
โ  โ      
โ  โโmerged_data (Combined 87 CSV into 1 CSV )
โ  โ      
โ  โโorigin (Raw data downloaded from Kaggle)
โ  โ              
โ  โโprocessed_data (original data after preprocess: drop NaN values)
โ  โ      
โ  โโtmp_data_for_exploration (data for exploration)
โ          
โโUseful Features (Calculation Sheet for feature restructuring)
โ  โ  .DS_Store
โ  โ  1.counterScore_late.csv
โ  โ  1.counterScore_mid.csv
โ  โ  1.counterScore_pre.csv
โ  โ  2.lineupCombo.csv
โ  โ  3.championWinRate_late.csv
โ  โ  3.championWinRate_mid.csv
โ  โ  3.championWinRate_pre.csv
โ  โ  4.championAttackDefenseScore_late.csv
โ  โ  4.championAttackDefenseScore_mid.csv
โ  โ  4.championAttackDefenseScore_pre.csv
โ  โ  5.championControlScore.csv
โ  โ  6.championGoldAbility_late.csv
โ  โ  6.championGoldAbility_mid.csv
โ  โ  6.championGoldAbility_pre.csv
โ  โ  
โ  โโinitial
โ          3.championWinRate_late.csv
โ          3.championWinRate_mid.csv
โ          3.championWinRate_pre.csv
โ          
โโ__pycache__
        ChampionIdMapping.cpython-39.pyc
        dataMapping.cpython-39.pyc
```
### Raw data features:
<table>
<thead>
<tr>
<th>Column name</th>
<th>Use das input</th>
<th>Path from Match-V5</th>
<th>type</th>
<th>description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>gameId</code></td>
<td>No</td>
<td>info/gameId</td>
<td>str</td>
<td>unique value for each match</td>
</tr>
<tr>
<td><code>matchId</code></td>
<td>No</td>
<td>metadata/matchId</td>
<td>str</td>
<td>gameId prefixed with the players region</td>
</tr>
<tr>
<td><code>gameVersion</code></td>
<td>No</td>
<td>info/gameVersion</td>
<td>str</td>
<td>game version, the first two parts can be used to determine the patch</td>
</tr>
<tr>
<td><code>gameDuration</code></td>
<td>No</td>
<td>info/gameDuration</td>
<td>int</td>
<td>game duration in seconds</td>
</tr>
<tr>
<td><code>teamVictory</code></td>
<td>No</td>
<td>info/teams[t]/win</td>
<td>int</td>
<td>Team victory, either 100 for blue, or 200 for red</td>
</tr>
<tr>
<td><code>team_100_gold</code></td>
<td>No</td>
<td>info/participants[]/goldEarned</td>
<td>int</td>
<td>Total gold earned by blue team</td>
</tr>
<tr>
<td><code>team_200_gold</code></td>
<td>No</td>
<td>info/participants[]/goldEarned</td>
<td>int</td>
<td>Total gold earned by red team</td>
</tr>
<tr>
<td><code>Player_id</code></td>
<td>Yes</td>
<td>info/participants/participantId</td>
<td>int</td>
<td>Player id ranging from 1 to 10 included</td>
</tr>
<tr>
<td><code>Player_{Player_id}_team</code></td>
<td>Yes</td>
<td>info/participants/teamId</td>
<td>int</td>
<td>Player team, either 100 for blue team, or 200 for red team</td>
</tr>
<tr>
<td><code>Player_{Player_id}_ban</code></td>
<td>Yes</td>
<td>info/teams[t]/bans[i]/championId</td>
<td>int</td>
<td>Player champion banned</td>
</tr>
<tr>
<td><code>Player_{Player_id}_pick</code></td>
<td>Yes</td>
<td>info/participants[i]/championId</td>
<td>int</td>
<td>Player champion picked</td>
</tr>
<tr>
<td><code>Player_{Player_id}_ban_turn</code></td>
<td>Yes</td>
<td>info/teams[t]/bans[i]/pickTurn</td>
<td>int</td>
<td>Player pick order</td>
</tr>
<tr>
<td><code>Player_{Player_id}_victory</code></td>
<td>No</td>
<td>info/teams[t]/win</td>
<td>int</td>
<td>Either 1 for victory or 0 for defeat</td>
</tr>
<tr>
<td><code>Player_{Player_id}_role</code></td>
<td>No</td>
<td>info/participants[i]/role</td>
<td>str</td>
<td>Role declared by the player before match. Possible values: DUO, DUO<em>CARRY, DUO</em>SUPPORT, NONE, and SOLO</td>
</tr>
<tr>
<td><code>Player_{Player_id}_position</code></td>
<td>No</td>
<td>info/participants[i]/teamPosition</td>
<td>str</td>
<td>Role deduced after match from every players position. Possible values: TOP, MIDDLE, JUNGLE, BOTTOM, UTILITY, APEX, and NONE</td>
</tr>
<tr>
<td><code>Player_{Player_id}_time_game</code></td>
<td>No</td>
<td>info/gameDuration</td>
<td>int</td>
<td>Game duration in seconds</td>
</tr>
<tr>
<td><code>Player_{Player_id}_gold</code></td>
<td>No</td>
<td>info/participants[i]/goldEarned</td>
<td>int</td>
<td>Total gold earned</td>
</tr>
<tr>
<td><code>Player_{Player_id}_xp</code></td>
<td>No</td>
<td>info/participants[i]/champExperience</td>
<td>int</td>
<td>Total XP accumulated</td>
</tr>
<tr>
<td><code>Player_{Player_id}_dmg_dealt</code></td>
<td>No</td>
<td>info/participants[i]/totalDamageDealtToChampions</td>
<td>int</td>
<td>Total damages dealt to other champions</td>
</tr>
<tr>
<td><code>Player_{Player_id}_dmg_taken</code></td>
<td>No</td>
<td>info/participants[i]/totalDamageTaken</td>
<td>int</td>
<td>Total damages received</td>
</tr>
<tr>
<td><code>Player_{Player_id}_time_ccing</code></td>
<td>No</td>
<td>info/participants[i]/timeCCingOthers</td>
<td>int</td>
<td>Total time of crowd control inflicted to other champs</td>
</tr>
</tbody>
</table>

## Features Formula Explanation:
```
A. Championโs Counter Score:
For Champion A vs B in this Position:
The counter score = 
โ (Player Who Pick Champ A in This Position_gold)- โ (Player Who Pick Champ B in This Position_gold) / Matches Champion A vs Champion B
For Champion B vs A in this Position: counter score = -(Counter Score A vs B)

B. Championโs win rate
N_win = Number of matches the champion won
N = Total number of matches in which the hero Champion was picked
Nโ_win = Number of matches the champion won in that position(Top, Jungle , Mid, Bottom, Utility)
Nโ = Total number of matches in which the hero Champion was picked in that position
championโs overall win rate = N_win / N
championโs win rate in each position = Nโ_win / Nโ
For rare champions with few matches at each position:
when the number of matches in which a hero is picked in that position is less than N/n (n = 160 , the number of all champions), we consider this champion to be a rare hero in that position and his win rate is inaccurate. 
We use the weighted average win rate in that position of all rare champions as the win rate of each rare champion in that position.

C. Championโs attack/defense ability
For each match:
dmg_dealt = total damages dealt by the champion to others
dmg_taken = total damages received by the champion
dmg_dealt_per_min = dmg_dealt / gameDuration * 60
dmg_taken_per_min = dmg_taken / gameDuration * 60
championโs attack ability = โ dmg_dealt_per_min / N  (
championโs defense ability = โ dmg_taken_per_min / N  Teamโs composition 
Mean_attack_ability = โ championโs attack ability / 5
Mean_defense_ability = โ championโs attack ability / 5
teamโs composition = Mean_attack_ability - Mean_defense_ability

D. Championโs control ability
For each match:
time_control = total time of crowd control inflicted to other champs (in seconds)
time_control_per_min = time_control / gameDuration * 60
championโs control ability = โ time_control / N  
```

### Compile enviornment:
- Windows System, VSCode, Python Version: 3.10.5 64bit
- Python Library Needed:
  * numpy  		1.23.2
  * pandas		1.4.4
  * scikit learn 		1.1.2
  * matplotlib		3.5.3
  * seaborn		0.12.1


 
