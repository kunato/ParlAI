# Dataset pattern
```
# https://parl.ai/docs/core/teachers.html
text: ?????? \t(tab only not space)labels: ?????
```
#### OR
```
text:Sam went to the kitchen. <NEWL>
Pat gave Sam the milk. <NEWL>
Where is the milk? <TAB> labels:kitchen <TAB> reward:1
<TAB> label_candidates:hallway|kitchen|bathroom
text:Sam went to the hallway. <NEWL>
Pat went to the bathroom. <NEWL>
Where is the milk? <TAB> labels:hallway <TAB> reward:1
<TAB> label_candidates:hallway|kitchen|bathroom <TAB> episode_done:True
```
#### OR
```
text:hello how are you today?	labels:i'm great thanks! what are you doing?
text:i've just been biking.	labels:oh nice, i haven't got on a bike in years!   episode_done:True
```

### with train val test split
```
# --fromfile-datatype-extension true
mydata_train.txt, mydata_valid.txt mydata_test.txt (In same folder)
```


# To Train

```
# https://parl.ai/docs/tutorial_torch_generator_agent.html
1. Define model (see tmp/example_model.py)
parlai train_model --model examples/seq2seq --model-file /tmp/example_model --task convai2 --batchsize 32 --num-epochs 2 --truncate 128

# Or mix the task option to train from file
parlai train_model --model examples/seq2seq --model-file /tmp/example_model --task fromfile:parlaiformat --fromfile_datapath ~/ParlAI/tmp/data.txt --batchsize 32 --num-epochs 2 --truncate 128

```



### Remark
```
episode_done:True (end of conversation) (reset the context)
```