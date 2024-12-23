・cuda、python3を使用できるdocker環境を構築します。
・nvidia-docker2がインストールされている必要があります。
・docker composeはバージョン2系が必要です。
・DockerfileのFROMにて必要なcuda+os環境を指定してください。
・「./home」にコンテナ内の「./home」がマウントされます。


(icecreamの使い方)
from icecream import ic
ic.configureOutput(includeContext=True)
ic(~)

(dockerコンテナのrootユーザからguiを使えるようにする)

許可
xhost +local:

非許可
xhost -local:

確認
xhost

(dockerコンテナ、イメージを全て削除)
docker compose down --rmi all --volumes --remove-orphans

（jupyterlabへのアクセス）
docker compose exec ubuntu-cuda bash -c "jupyter-lab --port=8888 --ip=0.0.0.0 --allow-root --NotebookApp.token=''"
http://localhost:8888

（tensorboardへのアクセス）
tensorboard --logdir ./data --host=0.0.0.0
http://localhost:6006

matplotlib日本語
plt.rcParams['font.family'] = 'IPAexGothic'

GPU クロック制限
nvidia-smi -q -d CLOCK
sudo nvidia-smi --lock-gpu-clocks=210,2500 ok
sudo nvidia-smi --reset-gpu-clocks

GPU W 制限
nvidia-smi -q -d POWER
sudo nvidia-smi -pl 300 ok
sudo nvidia-smi -pl 350 ok
sudo nvidia-smi -pl 400 ok
sudo nvidia-smi -pl 450

マルチGPU時の環境変数
- NCCL_P2P_DISABLE="1"
- NCCL_IB_DISABLE="1"
