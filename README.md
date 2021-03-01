# Code Snippet

파이썬 조각 코드 모음 <br/>
출처: [wikidocs](https://wikidocs.net/book/536), Stackoverflow, 기타 블로그


## [1] File IO

- [data를 pickle로 저장하기](https://wikidocs.net/8929)
- [glob - 특정 파일만 출력하기](https://wikidocs.net/3746)
- [절대경로, 상대경로, 현재경로](https://wikidocs.net/3716)
- [파일, 디렉토리 다루기](https://wikidocs.net/3717)

## [2] Python Image Library (PIL)

- [Font 다루기](https://wikidocs.net/12157)
- [간단한 PIL 예제](https://wikidocs.net/3702)
- [이미지 뒤집기](https://wikidocs.net/12205)

## [3] Thread & Multiprocessing

- [Thread](https://niceman.tistory.com/138?category=940952)
- [Multiprocessing](https://niceman.tistory.com/145?category=940952)

## [4] 기타 snippet

- [lambda, map, reduce, filter](https://wikidocs.net/64)
- [Decorator](https://velog.io/@doondoony/Python-Decorator-101)
- [Generator](https://wikidocs.net/16069)
- [Type Annotation](https://www.daleseo.com/python-typing/)
- [문자열 내 숫자 올바르게 정렬하기](https://stackoverflow.com/questions/5967500/how-to-correctly-sort-a-string-with-a-number-inside)
- [상위 경로의 파일 import하기](https://seongkyun.github.io/others/2019/04/29/python_import/)
- 코드 파일 실행 중간에 IPython 실행하기
  ```python3
  import IPython; IPython.embed(); exit(1)
  ```
  
- Argparser boolean type 지정
  ```python3
  def str2bool(v):
        if v.lower() in ('yes', 'true', 't', 'y', '1'):
            return True
        elif v.lower() in ('no', 'false', 'f', 'n', '0'):
            return False
        else:
            raise argparse.ArgumentTypeError('Boolean value expected.')
  # [Example] parser.add_argument('--option', default=True, type=str2bool)
  ```
  
## [5] PyTorch

- [pack_padded_sequence](https://simonjisu.github.io/nlp/2018/07/05/packedsequence.html)
  
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
