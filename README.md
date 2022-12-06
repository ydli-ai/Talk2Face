# Talk2Face: A Unified Sequence-based Framework for Diverse Face Generation and Analysis Tasks
**ACM MM 2022**
  
*Yudong Li, Xianxu Hou, Zhe Zhao, Linlin Shen, Xuefeng Yang and Kimmo Yan*


[Paper](https://dl.acm.org/doi/abs/10.1145/3503161.3548205)

## Useage


Our implementation is based on [TencentPretrain](https://github.com/Tencent/TencentPretrain).


```bash
git clone https://github.com/Tencent/TencentPretrain.git
cd TencentPretrain
```

Download the pre-trained [VQGAN](https://k00.fr/yndvfu95) and
[Talk2face](https://drive.google.com/file/d/1dG5EBIniHocKCqEB9QnFaZfsJmXxD0Mn) weights.
Install the VQGAN requirements.

```
pip install taming-transformers-rom1504
```



There are three modes for Talk2face to use shared model weights, namely {to_attributes},
{to_caption} and {to_image}. 

### To image

Given a text description, ask the model to generate the corresponding face images.
Write a text description to a file, e.g. 
*"This guy doesn't have any beard and has no fringe. He is in his middle age and has no smile."*
to `text.txt`.


```bash
python3 scripts/generate_talk2face.py --load_model_path talk2face.bin \
                    --config_path models/talk2face/base_config.json \
                    --vocab_path models/google_uncased_en_vocab.txt \
                    --vqgan_config_path ffhq_transformer/configs/2021-04-23T18-19-01-project.yaml \
                    --vqgan_model_path ffhq_transformer/checkpoints/last.ckpt \
                    --prompt to_image --text_prefix_path text.txt
```

Note that the results presented in the paper were filtered by CLIP. 
In this project, multiple results are generated according to the parameter `--samples_num`.
Users can choose with the help of CLIP or manually as the final output.

### To caption

Given a face image, ask the model to generate the text descriptions.

```bash
python3 scripts/generate_talk2face.py --load_model_path talk2face.bin \
                    --config_path models/talk2face/base_config.json \
                    --vocab_path models/google_uncased_en_vocab.txt \
                    --vqgan_config_path ffhq_transformer/configs/2021-04-23T18-19-01-project.yaml \
                    --vqgan_model_path ffhq_transformer/checkpoints/last.ckpt \
                    --prompt to_caption --image_prefix_path img.jpg
```

### To attributes

Given a face image and an attribute, ask the model to predict the value of the attribute.
Write an attribute to a file, e.g. *"gender: "* to `attribute.txt`. 
The model will predict the value as `male` or `female`.

```bash
python3 scripts/generate_talk2face.py --load_model_path talk2face.bin \
                    --config_path models/talk2face/base_config.json \
                    --vocab_path models/google_uncased_en_vocab.txt \
                    --vqgan_config_path ffhq_transformer/configs/2021-04-23T18-19-01-project.yaml \
                    --vqgan_model_path ffhq_transformer/checkpoints/last.ckpt \
                    --prompt to_attributes --image_prefix_path img.jpg \
                    --text_prefix_path attr.txt 
```

## BibTeX

```
@inproceedings{li2022talk2face,
  title={Talk2Face: A Unified Sequence-based Framework for Diverse Face Generation and Analysis Tasks},
  author={Li, Yudong and Hou, Xianxu and Zhao, Zhe and Shen, Linlin and Yang, Xuefeng and Yan, Kimmo},
  booktitle={Proceedings of the 30th ACM International Conference on Multimedia},
  pages={4594--4604},
  year={2022}
}
```
