# Code Snippet

파이썬 조각 코드 모음 <br/>
출처: [wikidocs](https://wikidocs.net/book/536), Stackoverflow, 기타 블로그


## 1. File IO

- [data를 pickle로 저장하기](https://wikidocs.net/8929)
- [glob - 특정 파일만 출력하기](https://wikidocs.net/3746)
- [절대경로, 상대경로, 현재경로](https://wikidocs.net/3716)
- [파일, 디렉토리 다루기](https://wikidocs.net/3717)

## 2. Python Image Library (PIL)

- [Font 다루기](https://wikidocs.net/12157)
- [간단한 PIL 예제](https://wikidocs.net/3702)
- [이미지 뒤집기](https://wikidocs.net/12205)

## 3. Thread & Multiprocessing

- [Thread](https://niceman.tistory.com/138?category=940952)
- [Multiprocessing](https://niceman.tistory.com/145?category=940952)

## 4. 기타 snippet

- [lambda, map, reduce, filter](https://wikidocs.net/64)
- [Decorator](https://velog.io/@doondoony/Python-Decorator-101)
- [Generator](https://wikidocs.net/16069)
- [Type Annotation](https://www.daleseo.com/python-typing/)
- [문자열 내 숫자 올바르게 정렬하기](https://stackoverflow.com/questions/5967500/how-to-correctly-sort-a-string-with-a-number-inside)
- [Python String Template](https://appia.tistory.com/244)
- [상위 경로의 파일 import하기](https://seongkyun.github.io/others/2019/04/29/python_import/)
- [Python setup.py](https://data-newbie.tistory.com/770)
- [YAML](https://rfriend.tistory.com/540)
- 코드 파일 실행 중간에 IPython 실행하기
  ```python3
  import IPython; IPython.embed(); exit(1)
  ```
  
- [nohup background run](https://joonyon.tistory.com/entry/%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85%ED%95%9C-nohup-%EA%B3%BC-%EB%B0%B1%EA%B7%B8%EB%9D%BC%EC%9A%B4%EB%93%9C-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%82%AC%EC%9A%A9%EB%B2%95) (+ [kill process](https://velog.io/@jekim5418/Shell-Script-nohup%EC%9C%BC%EB%A1%9C-%EC%8B%A4%ED%96%89%ED%95%9C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%A2%85%EB%A3%8C))
  ```sh
  $ nohup ./my_shellscript.sh &
  ```
  
- Argparser boolean type 지정
  ```python3
  # Diverse boolean form
  def str2bool(v):
        if v.lower() in ('yes', 'true', 't', 'y', '1'):
            return True
        elif v.lower() in ('no', 'false', 'f', 'n', '0'):
            return False
        else:
            raise argparse.ArgumentTypeError('Boolean value expected.')
  parser.add_argument('--your_arg', default=True, type=str2bool)
  
  # Flagging form
  parser.add_argument("--your_arg", action="store_true", default=False)
  ```
  
 - Join list of lists
    ```python3
    import itertools
    a = [['a','b'], ['c']]
    print(list(itertools.chain.from_iterable(a)))
    ```
    
- Print formatted time
  ```python3
  import time
  def check_time(start_time: float) -> str:
    sec = time.time() - start_time
    times = str(datetime.timedelta(seconds=sec)).split(".")
    return times[0]
  # start_time = time.time()
  # total_time = check_time(start_time)
  ```

- JSON load & save
  ```python3
  import json
  # load
  with open("./name.json", "r") as json_file:
      data = json.load(json_file)
    
  # save with indent
  with open("./name.json", "w") as json_file:
      json.dump(your_json, json_file, indent=4)
  ```
  
## 5. PyTorch

- [pack_padded_sequence](https://simonjisu.github.io/nlp/2018/07/05/packedsequence.html)
- [Simple lazy loading dataset](https://discuss.pytorch.org/t/loading-huge-data-functionality/346/3)
  
- PyTorch Seed 고정
  ```python3
  import random
  import torch
  import numpy as np
  
  def fix_seed(seed: int) -> None:
    torch.manual_seed(seed)
    torch.cuda.manual_seed(seed)
    torch.cuda.manual_seed_all(seed)
    torch.backends.cudnn.deterministic = True # this can slow down speed
    torch.backends.cudnn.benchmark = False
    np.random.seed(seed)
    random.seed(seed)
  ```

- Number of parameters
  ```python3
  num_params = sum(p.numel() for p in net.parameters() if p.requires_grad)
  ```
  
- Sync checkpoint parameter name 
  ```python3
  # original saved file with DataParallel
  state_dict = torch.load('myfile.pth.tar')
  # create new OrderedDict that does not contain `module.`
  from collections import OrderedDict
  new_state_dict = OrderedDict()
  for k, v in state_dict.items():
      name = k[7:] # remove `module.`
      new_state_dict[name] = v
  # load params
  model.load_state_dict(new_state_dict)
  ```
