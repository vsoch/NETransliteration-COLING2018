# Tensorflow experimental (with containers)

To replicate the study fully, please see the [README.md](../README.md) that describes
setting up resources with AWS Deep Learning. This description will generate (to the
best of the author's ability) a comparable environment that is agnostic to the host
provider, and requires Docker (or Singularity) container technologies.

You will be building the container from the [root of the repository](../) and direct to the
Dockerfile that you want, depending on needing (or not being able to use) GPU.

```bash
# no GPU
docker build -t vanessa/netransliteration-coling2018-cpu -f docker/Dockerfile .

# no GPU
docker build -t vanessa/netransliteration-coling2018-gpu -f docker/Dockerfile.gpu .
```

## Versions

 - tensorflow: 1.5.0
 - python 3.5.2


# Usage (shell)

```bash
docker run -it --name ntc-cpu vanessa/netransliteration-coling2018-cpu bash
```

## Training and Testing


```bash
cd /code/scripts
```

Here are the data files that we can use for training:

```bash
# ls ../data/
LICENSE                                wd_japanese_20
wd_arabic                              wd_japanese_64
wd_arabic.normalized.aligned.tokens    wd_japanese_80
wd_arabic_16                           wd_katakana
wd_arabic_20                           wd_katakana.normalized.aligned.tokens
wd_arabic_64                           wd_katakana_16
wd_arabic_80                           wd_katakana_20
wd_chinese                             wd_katakana_64
wd_chinese.normalized.aligned.tokens   wd_katakana_80
wd_chinese_16                          wd_korean
wd_chinese_20                          wd_korean.normalized.aligned.tokens
wd_chinese_64                          wd_korean_16
wd_chinese_80                          wd_korean_20
wd_hebrew                              wd_korean_64
wd_hebrew.normalized.aligned.tokens    wd_korean_80
wd_hebrew_16                           wd_russian
wd_hebrew_20                           wd_russian.normalized.aligned.tokens
wd_hebrew_64                           wd_russian_16
wd_hebrew_80                           wd_russian_20
wd_japanese                            wd_russian_64
wd_japanese.normalized.aligned.tokens  wd_russian_80
wd_japanese_16
```

```
/bin/bash /code/scripts/train.sh /code/data/wd_arabic /code/models/arabic_t2t_1 t2t
```

**Stopped here, multiple errors and still trying to debug**
