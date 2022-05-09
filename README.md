# facedetectir-on-deepstream
facedetectir-on-deepstream は、DeepStream 上で FaceDeteceIR の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- FaceDeteceIR
- Docker
- TensorRT Runtime

## FaceDeteceIRについて
FaceDeteceIR は、画像内の顔をを検出し、カテゴリラベルを返すAIモデルです。  
FaceDeteceIR は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、FaceDeteceIR の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の FaceDeteceIR でストリーミングを開始します。  
```
stream-start: ## ストリーミングを開始する
	xhost +
	docker exec -it deepstream-facedetectir deepstream-app -c /app/src/deepstream_app_source1_facedetectir.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために FaceDeteceIR の AIモデルを最適化する手順は、[facedetectir-on-tao-toolkit](https://github.com/latonaio/facedetectir-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである facedetectir.engine は、[facedetectir-on-tao-toolkit](https://github.com/latonaio/facedetectir-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  
