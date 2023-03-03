FROM runpod/stable-diffusion:web-automatic-1.5.16

SHELL ["/bin/bash", "-c"]

ENV PATH="${PATH}:/workspace/stable-diffusion-webui/venv/bin"

WORKDIR /

RUN git clone https://github.com/Mikubill/sd-webui-controlnet.git /workspace/stable-diffusion-webui/extensions/sd-webui-controlnet/

RUN wget -O /workspace/stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_sd15_openpose.safetensors https://civitai.com/api/download/models/11017
RUN pip install -U xformers
RUN pip install runpod
RUN   sed -i "s|}|\"control_net_model_config\": \"models\\\\cldm_v15.yaml\",\r\n    \"control_net_model_adapter_config\": \"models\\\\sketch_adapter_v14.yaml\",\r\n    \"control_net_detectedmap_dir\": \"detected_maps\",\r\n    \"control_net_models_path\": \"\",\r\n    \"control_net_max_models_num\": 1,\r\n    \"control_net_model_cache_size\": 2,\r\n    \"control_net_control_transfer\": false,\r\n    \"control_net_no_detectmap\": false,\r\n    \"control_net_detectmap_autosaving\": false,\r\n    \"control_net_only_midctrl_hires\": true,\r\n    \"control_net_allow_script_control\": true,\r\n    \"control_net_skip_img2img_processing\": false,\r\n    \"control_net_monocular_depth_optim\": false,\r\n    \"control_net_only_mid_control\": false,\r\n    \"control_net_cfg_based_guidance\": false\r\n} |g" /etc/sysctl.conf

ADD handler.py .
ADD start.sh /start.sh
RUN chmod +x /start.sh

CMD [ "/start.sh" ]
