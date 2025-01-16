# 네트워크 상에서 Timeout 처리

### 예시 상황

> 1. A와 B 프로그램이 TCP 연결을 통해 통신할 때,
> 2. A가 요청을 보냈지만, B에서 요청을 처리하는데 너무 많은 시간이 걸린다.
> 3. 그래서 A에서 timeout 처리를 했다.
> 
> 이때 해당 요청에 대한 패킷은 어떻게 할까?

### **A 관점**

- 타임아웃 시, A는 해당 요청에 대한 처리를 중단하고 사용자에게 오류를 알리거나 재시도합니다.
- A는 연결을 종료하기 위해 **FIN** 패킷(4WH)을 보내는 것이 일반적이며, 특정 상황에서는 **RST** 패킷을 전송하여 연결을 강제로 종료합니다.

### B관점

- A로 전송하려 할 때, A가 이미 연결을 종료한 상태라면
- B의 응답 패킷은 A에 도달하더라도 무시되거나 **RST** 패킷으로 응답받을 수 있습니다.

### 패킷 관점

- A가 타임아웃 후 연결을 종료하면, 이후 B로부터 오는 해당 요청에 대한 응답 패킷은 A에서 유효하지 않은 세션으로 간주되어 폐기됩니다.

### 관련 자료

네트워크 상에서 Timeout 처리

[TCP 재전송과 타임아웃](https://ghdwlsgur.github.io/docs/Linux/devops_se_ch_9)