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

#### OR JSON 
```

    Conversations should be saved in JSONL format, where each line is
    a JSON of the following form:
    WARNING: The data below must be on ONE LINE per dialogue
    in a conversation file or it will not load!!
    .. code-block:
        {
            'possible_conversation_level_info': True,
            'dialog':
                [   [
                        {
                            'id': 'speaker_1',
                            'text': <first utterance>,
                        },
                        {
                            'id': 'speaker_2',
                            'text': <second utterance>,
                        },
                        ...
                    ],
                    ...
                ]
            ...
        }
    """
```
```
--jsonfile-datapath /tmp/data.json
```
```
# Hardcoded metadata
{
    "version": "0.1",
    "self_chat": false,
    "speakers": null,
    "opt": {},
    "date": "2021-07-11 18:10:43.039242"
}
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
```
## Train command (latest)
```
parlai train_model --model examples/seq2seq --model-file /tmp/example_model --task jsonfile --jsonfile-datapath tmp/out/bd_episode --jsonfile-datatype-extension true --batchsize 32 --num-epochs 2 --truncate 128
```



### Remark
```
episode_done:True (end of conversation) (reset the context)
```