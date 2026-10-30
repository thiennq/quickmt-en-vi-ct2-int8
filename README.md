# quickmt-en-vi, CTranslate2 int8

English → Vietnamese translation model [quickmt/quickmt-en-vi](https://huggingface.co/quickmt/quickmt-en-vi), with its weights converted from float16 to int8 for [CTranslate2](https://github.com/OpenNMT/CTranslate2). It loads faster and needs less memory on small devices (it is used on a 32-bit Android TV). Translations are identical to running the original model with `compute_type="int8"`.

The model files are attached to the [v1 release](../../releases/tag/v1).

## License

The original model is by quickmt and licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This copy is licensed under CC BY 4.0 as well. See [NOTICE.txt](NOTICE.txt) for the changes made.

## Files (release v1)

| File | Bytes | SHA-256 |
|------|------:|---------|
| `model.bin` | 206686329 | `81f2be8df576c8c28505a71466f45db172aebbf74b64b05045321dc308d023a0` |
| `config.json` | 223 | `66edc5d58ceb812a41b4b784497001f815c35400884f40984b19de29e1bc3d69` |
| `source_vocabulary.json` | 335066 | `6742782136af6e207fb86f650f60a556f187ab18e9da405b22dec7b45384a2a5` |
| `target_vocabulary.json` | 322073 | `580d7293caa7cb66f4b427b5c929c17aec37396976ba0385c5124b512b65fd7a` |
| `src.spm.model` | 586058 | `82efd76a945ec4574b2ab3d2476b0043a9737c8dbe693cd20a7fa036d273c0eb` |
| `tgt.spm.model` | 553521 | `03be7f771990d2bee00d7ff09219baad95b53fef1dcd387b3048c156d665e046` |

## Usage

```python
import ctranslate2, sentencepiece as spm

translator = ctranslate2.Translator("quickmt-en-vi-ct2-int8", compute_type="int8")
src = spm.SentencePieceProcessor(model_file="quickmt-en-vi-ct2-int8/src.spm.model")
tgt = spm.SentencePieceProcessor(model_file="quickmt-en-vi-ct2-int8/tgt.spm.model")
tokens = src.encode("We need to reach the old lighthouse before nightfall.", out_type=str)
print(tgt.decode(translator.translate_batch([tokens], beam_size=1)[0].hypotheses[0]))
```
