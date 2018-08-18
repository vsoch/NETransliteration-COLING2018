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

# Usage (shell)

```bash
docker run -it --rm vanessa/netransliteration-coling2018-cpu bash
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

## Debugging

With the following versions:


 - tensorflow: 1.4.1
 - tensor2tensor: 1.7.0
 - python: 3.5.2

```bash
root@97ea517ebf53:/code/scripts# /bin/bash /code/scripts/train.sh /code/data/wd_arabic /code/models/arabic_t2t_1 t2t
Training with tensor2tensor
/code:
/usr/local/lib/python3.5/dist-packages/h5py/__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
Traceback (most recent call last):
  File "../xlit_t2t/app.py", line 32, in <module>
    from xlit_t2t.g2p import G2PModel
  File "/code/xlit_t2t/__init__.py", line 22, in <module>
    from xlit_t2t import g2p
  File "/code/xlit_t2t/g2p.py", line 28, in <module>
    from xlit_t2t import g2p_trainer_utils
  File "/code/xlit_t2t/g2p_trainer_utils.py", line 27, in <module>
    from tensor2tensor.utils import input_fn_builder
ImportError: cannot import name 'input_fn_builder'
```

The error seems to be for tensor2tensor > 1.3.2 (see [issue here](https://github.com/cmusphinx/g2p-seq2seq/issues/107#issuecomment-379718035))

 - tensorflow: 1.4.1
 - tensor2tensor: 1.3.2
 - python: 3.5.2

```bash
root@97ea517ebf53:/code/scripts# /bin/bash /code/scripts/train.sh /code/data/wd_arabic /code/models/arabic_t2t_1 t2t
Training with tensor2tensor
/code:
/usr/local/lib/python3.5/dist-packages/h5py/__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
Traceback (most recent call last):
  File "../xlit_t2t/app.py", line 137, in <module>
    tf.app.run()
  File "/usr/local/lib/python3.5/dist-packages/tensorflow/python/platform/app.py", line 48, in run
    _sys.exit(main(_sys.argv[:1] + flags_passthrough))
  File "../xlit_t2t/app.py", line 112, in main
    params = Params(FLAGS.model_dir, file_path, flags=FLAGS)
  File "/code/xlit_t2t/params.py", line 46, in __init__
    self.train_steps = len(open(data_path).readlines()) * flags.max_epochs
  File "/usr/lib/python3.5/encodings/ascii.py", line 26, in decode
    return codecs.ascii_decode(input, self.errors)[0]
UnicodeDecodeError: 'ascii' codec can't decode byte 0xd9 in position 8: ordinal not in range(128)
```

This is likely an issue with the format / data type of an input file. 

**Stopped here, multiple errors and still trying to debug**
