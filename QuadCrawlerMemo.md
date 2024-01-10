## クアッドクローラー歩行改善メモ

### クアッドクローラーでの実装テスト  

* 改善前(脚引きずり歩行)  
奥側の脚を引きずっている。  
https://sohtamei.github.io/docs/images/V_20200823_175859.mp4
<video src="https://sohtamei.github.io/docs/images/V_20200823_175859.mp4" controls></video>
  

* 3点接地  
早くならない＆前後左右旋回の方向切り替え時のモーションの繋ぎを実装するのが大変なので断念。  
https://sohtamei.github.io/docs/images/V_20200823_175609.mp4
<video src="https://sohtamei.github.io/docs/images/V_20200823_175609.mp4" controls></video>
  

* 2点接地(腹ずり)による歩行改善テスト１  
https://sohtamei.github.io/docs/images/V_20200824_204042.mp4
<video src="https://sohtamei.github.io/docs/images/V_20200824_204042.mp4" controls></video>
  

* 2点接地(腹ずり)による歩行改善テスト２  
https://sohtamei.github.io/docs/images/MAH05078s.mp4
<video src="https://sohtamei.github.io/docs/images/MAH05078s.mp4" controls width="894" height="415"></video>
  

### 改善前の脚引きずり歩行、剛性不足により歩かない不具合解析  

不具合例  
https://sohtamei.github.io/docs/images/vid_20200312_192803_ac9d0207f7b94s.mp4
<video src="https://sohtamei.github.io/docs/images/vid_20200312_192803_ac9d0207f7b94s.mp4" controls width="640" height="360"></video>

静力学的には下記のようになります。(右前と左後を上げている状態）  
動画のデモ機では重心が右に寄っているようですが、ロボットの重さのほとんどは下げている右後と左前にかかります。この重さがほとんどかかってない状態で剛性の不足により右前が動かない（滑らない）のが今回の問題の原因と思われます。砂川さんご提案のように右後、左前を伸ばすことは可能ですが、ロボットの重心位置が高いため右後、左前を伸ばすとロボットの傾きが大きくなり、右前にかかる分力はより大きくなります。症状としては悪化するはずです。  
![image](https://github.com/sohtamei/docs/assets/43091864/4689b030-327e-48a2-b1d8-6fcb1307a7f9)

### 市販ロボットでの実装例  

https://www.instructables.com/DIY-Spider-RobotQuad-robot-Quadruped/  

https://youtu.be/LB8VLnVpoPY?t=331  

https://www.youtube.com/watch?v=HzOQ39LhVOw&feature=emb_logo  

歩いてる時間が短すぎてよく分からず  
https://youtu.be/ijBc1u1R0ZM?t=17  
