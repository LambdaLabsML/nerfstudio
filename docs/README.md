# NERF Demos


## Installation


### clone and build the docker image
```
git clone https://github.com/chuanli11/nerfstudio.git && \
cd nerfstudio && \
git checkout lambda

docker build . -t chuanli11/nerfstudio:latest

docker login
docker push chuanli11/nerfstudio:latest
```

### Launch a interactive session

```
docker run --gpus all \
-v /home/ubuntu/ml/chuan/code/nerfstudio/data:/workspace/ \
-v /home/ubuntu/.cache/:/home/user/.cache/ \
-p 7007:7007 \
--rm \
-it \
chuanli11/nerfstudio:latest
```


### Process data (using a video example)

```
ns-process-data video \
--data nerfstudio/deyoung/C0039.MP4 \
--output-dir nerfstudio/deyoung/C0039_processed \
--verbose \
--num_frames_target 100 \
--matching_method sequential
```

### Launch localtunnel so the viewer is public

```
lt --port 7007 &
# keep the url and change https://<site-name> to wss://<site-name>
```


### Launch NERF training

```
ns-train nerfacto \
--data nerfstudio/deyoung/C0039_processed
```


### In any browser, go to this url to view

```
https://viewer.nerf.studio/?websocket_url=wss://<site-name>
```
