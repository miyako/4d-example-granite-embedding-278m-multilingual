## [ibm-granite/granite-embedding-278m-multilingual](https://huggingface.co/ibm-granite/granite-embedding-278m-multilingual)

|`max_position_embeddings`|`hidden_size`|`num_hidden_layers`|`pooling`
|-:|-:|-:|-:|
|`512`|`768`|`12`|`cls`

```4d
var $en; $fr : 4D.Vector
var $AIClient : cs.AIKit.OpenAI
var $cosineSimilarity : Real
$AIClient:=cs.AIKit.OpenAI.new()

$AIClient.baseURL:="http://127.0.0.1:8080/v1"  

$en:=$AIClient.embeddings.create("How do I reset my password?").embedding.embedding
$fr:=$AIClient.embeddings.create("Comment réinitialiser mon mot de passe?").embedding.embedding

$cosineSimilarity:=$en.cosineSimilarity($fr)

ALERT([$cosineSimilarity].join())
```

##### Cosine similarity from example code above:

|llama.cpp `Q8_0`|ONNX Runtime `Int8`|CTranslate2 `Int8`
|-|-|-|
|`0.76550467452203`|`0.73646691085979`|`0.76624839443032`
