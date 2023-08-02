# Kubernetes Example

## 添加cluster和context

### 环境说明

| 项 | 说明 |  
| ---- | ---- |
| kubernetes1 | 192.168.0.101 |
| kubernetes2 | 192.168.0.102 |
| mac-pro | 笔者的笔记本电脑，用来添加Cluster和设置context |

### 配置文件

#### kubernetes1 配置文件

~/.kube/config 内容如下：

```yaml
apiVersion: v1
kind: Config
clusters:
- cluster:
    api-version: v1
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN3akNDQWFxZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFTTVJBd0RnWURWUVFERXdkcmRXSmwKTFdOaE1CNFhEVEl4TURjeE5URXpOVEUxTVZvWERUTXhNRGN4TXpFek5URTFNVm93RWpFUU1BNEdBMVVFQXhNSAphM1ZpWlMxallUQ0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQ0FRb0NnZ0VCQU1PcFJVRzFaZm5NClcwc1pHamtBZ0dJcTg0UDlwTzh6RGxnc2RHUWJtQ0FYNUN0d3Mza0VXZzJVYnlYZUhhNDhxV09NRTVpNHpsZHEKMDl2QXZkeitoWHVjOHE0c0xqRjhFdW5jaEJhd002T1YrY04wbHlEOE0xcEUwelRoenRhYnZUQllhVVNuZmovbgpjditrWUlDNUdQRDRMdjFTWXBYOTdSK2R2TzdGaVg0a0t1d1p4ZVVETHdmQmN4NVdXaEdIT0tBQ0lFdHU5bkRyCkJTbnV2dE9lQ0kwUktrdzQwQ2pnMjVlYzVsT01paW1lNmpFdW5IZ0VpSkhmM0FtaGpSa0tmNVdaS2UreEpweDEKYjhIUFAvUXVJVnZSQVViOFA2VThUdGlmbVFRc0ZOMFZVK3h1QmN1b250UXFGVXFxQSt3MUtGUDBMOGVseHFIQgpESGc4elhhYXJDOENBd0VBQWFNak1DRXdEZ1lEVlIwUEFRSC9CQVFEQWdLa01BOEdBMVVkRXdFQi93UUZNQU1CCkFmOHdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBRk9ucGtjVmR5cW9JdUplZGNVWE9KK0Y3R0ViRkNCcytlcVkKLzBaMUZqNjQxZTJqZC9MNU9LMVJYTXF6ZEhIUm5WaEtUeXJDcWhXR2RLc2VjMmRrU1VBanh1TC9vQ1B1NldDMApaYkFPQXNCMXZuZW5WUTN0Y2h6OWU3ZnZ2b0dRWUV4NnpsMEVlcHA2N09EYUZIbHhsUGxINnN1dXhRM0VUQW9NCmV5UStBbHF0N0pwT3dzNEZRM3BBY1BOc2ZzZ0ZGQkJ0cjlPbDBMQm1xZUpBazlUN01LdHZSYnE2dkRsMWVTdFQKc05jMkdNaXpxUjY1QnQxc1B6QjF1VjdFditLVElFd1g3Vm84Um15ZjMrQjkzanBicHgrVEk1dGxxUXN6ZExUdgpod3pDQnhvZDJpcE9wdjU1Sm9ycmNsZ0RuOHFobTlYWVJXTk4vM2IzdGd2R1MvK1lKK1E9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: "https://192.168.0.101:6443"
  name: "local"
contexts:
- context:
    cluster: "local"
    user: "kube-admin-local"
  name: "local"
current-context: "local"
users:
- name: "kube-admin-local"
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM2VENDQWRHZ0F3SUJBZ0lJQ2RkVkJSRG9IM2t3RFFZSktvWklodmNOQVFFTEJRQXdFakVRTUE0R0ExVUUKQXhNSGEzVmlaUzFqWVRBZUZ3MHlNVEEzTVRVeE16VXhOVEZhRncwek1UQTNNVE14TkRFM016VmFNQzR4RnpBVgpCZ05WQkFvVERuTjVjM1JsYlRwdFlYTjBaWEp6TVJNd0VRWURWUVFERXdwcmRXSmxMV0ZrYldsdU1JSUJJakFOCkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQTJVYUpHMEN0VmhhS0hSeExURnFwbjlNaUcrUG8KdlZ6UGxZcXg0MXBCNk1DMmc1cHJ1MjBvdEwxWmxITkRFL01PQzNNNTVibjR0RDFzZUF5MjQ1ZEEzQUV6cml0UgovUEhNRzF3Ky9ZTTZiOTFQajd3cUd5UUE1dUNPTE1WbUYxQm5JbTRrSlNQUlNvRDFsZHMzcWFZeGl5VlpOT1VDClpXckR6NDh4Ry8wcG5PNDZNRGFNZ0VWS2VDU0ZhNm0zYjFaR1FWcEpqVi9HdVQ2QzhwOExucVBST0QzbkF3OXkKa1JnVm92MnlodGFwZXR6aDdVV2tTWHM3Vk5Gei9hM3pMT3FjQUdJa0plLzNXQ29iMTBPVG5Rbmg1Mms4SmphSgpzUm9JN2RLMURXMS9nT3crZDNKK2RkU0hYQTlreXF6UkZlWXJzaitRQTJHcFdab3RXbEJoWHVQWEJRSURBUUFCCm95Y3dKVEFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUhBd0l3RFFZSktvWkkKaHZjTkFRRUxCUUFEZ2dFQkFMejNNOWRxNzJvSENkSW16ODIzMXNuY0N6ZVI2QlFFQUhWOVlzR3RqSnl0Nm54UAo2bW1ORVE2eCtpSjhSenRHanVwb2Z2aGtwdS91VGZ0MUtYbm1yaHg5N1FQbWtqaXZSVnVoMGxjVE01aWVldXZSCmxONklqbzgwUVBuR2c5Q0tMWndONHZmTnBPbUg3a2J4VzJDOWJWVmRyb1VjQmZ3QmJ1ejFtQjNnVVVYYlovMlAKL3lsRStpTW5OQ0xseGtFYXMrZnpoL0VmTzVLRE8wY0xFMDJIaEV2WEI1WkFEZUViZzlRdHFMNkZwOW9pVTRYbgpXcTR5Z1llV2NLWndyZ0hWWXpaOXQ5RkdlQUNnM0FLWHdwcDhDN3lDSE1EUWpmcnBsQzI5QU1WN2RHWjZ4azI0CmxSU3JiRVA4NVF1M0tUOUZyS0NaY3E1OWd2bm0xUEREVHJLaVI4VT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcEFJQkFBS0NBUUVBMlVhSkcwQ3RWaGFLSFJ4TFRGcXBuOU1pRytQb3ZWelBsWXF4NDFwQjZNQzJnNXByCnUyMG90TDFabEhOREUvTU9DM001NWJuNHREMXNlQXkyNDVkQTNBRXpyaXRSL1BITUcxdysvWU02YjkxUGo3d3EKR3lRQTV1Q09MTVZtRjFCbkltNGtKU1BSU29EMWxkczNxYVl4aXlWWk5PVUNaV3JEejQ4eEcvMHBuTzQ2TURhTQpnRVZLZUNTRmE2bTNiMVpHUVZwSmpWL0d1VDZDOHA4TG5xUFJPRDNuQXc5eWtSZ1ZvdjJ5aHRhcGV0emg3VVdrClNYczdWTkZ6L2EzekxPcWNBR0lrSmUvM1dDb2IxME9UblFuaDUyazhKamFKc1JvSTdkSzFEVzEvZ093K2QzSisKZGRTSFhBOWt5cXpSRmVZcnNqK1FBMkdwV1pvdFdsQmhYdVBYQlFJREFRQUJBb0lCQUVXbDVxMWx2aXFxYnZ1Rgo1bDFEY3J4WTRjWXUrSnc2OUEvcnRibzdaSVZId1RuT2RscE9VNDRjWkdyQngrN05LdU5ndkY1M2p0RzRIdDBjCnRrT2VhSndkaG9OK1Azbmx5SmU4cWpSNXJISFBiNEdUdjZ1VGp2WnpaUi9VNXpUeUFSMTRVUDNXelhBa2hwVFQKQUxUUklYQ0pPRjlNU2NoWXdRdjN5clkrSU9pOG5WZWNTTzFQWEtURlN0QUFoQitiNzFUeEdNbituOVUzNkw2YgpWb2kzdnhOTHpvRUttNlZvV2FhanFzUm4xTEdEU0RVcm80LzF2Y2Y4clc4NHlSSGREb2U3d1l3dWFUV3VYc1NICk54OCt1UnpucExCTTN3OFFmNTgvNkZlN1dVMVZDL0J6Z0RhZkMzT0hlS3p5eWUwRTFCaTVuU2N5aFV4VWxES1QKTnFvNE1BRUNnWUVBK2EzYlo2REtkUkdabmo0cWY4NVlCNmtzbzJCc293Z2orNHRTbVJEQkpoV2M1b1BqTk5wNQp6QS9iNGtjUGc4b1hNZlRzNkEvN1FDQk0rSytnRmk3R211akVPVmQrb2tLeTdDNnpmZnVPWHB6ZWVmS1hKM3JZClczbHRNQks2TEYrUDJQc3ZyYmtYb2RtTUNGditRcjlnOWhFQkFydWxRaVp6SVhSVWJ6aVM4TUVDZ1lFQTNzYXMKb3VkZmFvRTYrQk50YktqOGdLNENsbkZMaVoyMCtQNWFiRVFDOEdsRmlabjMxV2NGUHFzbGdEWXhTL3lGQ0dLUAphcFdiNDlZRjRMMnl0YXhmUlhneXc0VWlHNFJRSXlVVDhJSFRXQTkwdFFxb3dBc3NQeHBUR1hTMWRQTXNJQUlGCkFDLzU1ZDVQV1hReVJqTSt6MzVmUEZzOHZRQ0l1TUNuYU90eXMwVUNnWUVBK1VTR2VHWUIybkRRMGpnMFM5YWcKOGowR3NMRnlwQzFiWnlYSU44S1BZc3RQRXFCM2RHdnVEem1DQjkxejh0b080RFFyVk4rbnNuVE5BN2FxOTVxSgpjMXlSa3NIMFRtQ1NxdE5SSmFUQWxWcTlqamdRaWp6TnhqMXJNZ1J3VkI2dnlTdTFoUlgyTHdLM0dCMW5zaEhJCjVzRkJKZzVheGJrSFZrNENnZXVVWDhFQ2dZQXA2b0hUQ091NEUyYXdCSi9ESVN5WlhhUlpBQ294VTM0WWwyc1cKRWRubnVEY0FRL3NRcVJpZ2lQMCtXWFAvRXgxSXpacWtlRS9qbDRKMW5kdkJPUlNYOHB6Q2t3c3UyRDluelhNcAovcE53YjBBTFRGMGgvVGd2QzFuMVlUTS9OUDNwYTlmYkNDdmg1MmxRc0g5QkhDVkdUMFhHQ25pc0t5eU9icGxSCk1YUGNiUUtCZ1FEcXg0ODhyc2krT0Jlci81MHNWZE1lTWNsSzFEaVZER013VFR3ZmZBRFFlT1BaN00xaitaU04KRVhYMHpGZGN4Mk81TU1hWkFNY01DMHl6Nm9HV0lVODRWT3AxWjNoOGV5dS9Ec3F0Y1ZIUkxDSmcrWWlVZkR6QgpuKzFXeEtkTmVUc1h6L01JMi9QNlQyQ2NSUHRyT2JScTBDUzdidDgzVzlqZmdsRm5CeStwc0E9PQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
```

#### kubernetes2 配置文件

~/.kube/config 内容如下：

```yaml
apiVersion: v1
kind: Config
clusters:
- cluster:
    api-version: v1
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN3akNDQWFxZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFTTVJBd0RnWURWUVFERXdkcmRXSmwKTFdOaE1CNFhEVEl4TURjeE5URTFNVGd5T0ZvWERUTXhNRGN4TXpFMU1UZ3lPRm93RWpFUU1BNEdBMVVFQXhNSAphM1ZpWlMxallUQ0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQ0FRb0NnZ0VCQUs1WjdRSUNpM3dLCkhsbUZvYXJ1SVdqK2VwVnpkUjRtN2VsQnk3dGUxMWt0TzZ6VDRpbGZaODV3RDRlYzRSZmJGVDVwaDNJbDFCQkcKNnRhTXpSWEVoRFhGdHN5eWZhbEVOcVRETlV0SC8zaFZKZjZxbnk2SE1YV0hzdWlkZ3d1MXlYZG9Ka3dDbjVEbwowUjN1dEowTVBvenZoSzhOeHZJRk1xUjN4NjF0Y2RGUjF3RFVTeGlxeDdoQWtLQjBqUkkzSEJyR05QcDlwTTBtCjlnK1RWQm1WOUl2TkR0VUprNG5YWEVkbS9BOVJzQmNUWjVDVC9SbjQxN0NhbkwzdTJpTlU0UHVCUjZUMDB1bFAKbFRSRERwQ3Y1d1N0TWxLV3EzeHRiWE5Xa2JmU3dTUiswZ2M3WDR2WGVWS2hwdmNLL3FwbEtuSU1KcVZoc1ZINApHdTExTldBM05IRUNBd0VBQWFNak1DRXdEZ1lEVlIwUEFRSC9CQVFEQWdLa01BOEdBMVVkRXdFQi93UUZNQU1CCkFmOHdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBRWVHWUR2djM0bXZxNDRFUXRFdlBhM1V5V05iL0paOTUzWncKd1dId2d0S2dBd3RvbG5xdG9iMUJzdktBVE00VUEwbWNjVThpL0tmTFMvNVZxaC9vK0NGNjhnMmtEendnS2U3aApydWxOOTE2RWIwOS82M2NHYlhCV0xuT0JxNmRlT3NhcVN4dzNkYmtWN1pGQy9GS3IvOWNOYndmMXhRa1NvRDlXCjRtVnJPNzRMQlRHQk9OMFhxanllVmYwbnBMTlZZUzVsZEU1UHhaM21QZk5oOWptcWpVcjBJZ2ViZHJVZm54QU8KaHZEOHJGbE1QTUlaWEdkTjlZUHBxb2srVTY0SnA1NHhkNWNiYk5XaXdYYXRJYjV4dnoremZ5VFluYXJlUmtoKwpFd3Rtd3VZMitra1pkelpTdTFKSXBua0ZNTUhQRzI0b2k5RzBvekpsUDIwcE5iMFVHWUU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: "https://192.168.0.102:6443"
  name: "local"
contexts:
- context:
    cluster: "local"
    user: "kube-admin-local"
  name: "local"
current-context: "local"
users:
- name: "kube-admin-local"
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM2VENDQWRHZ0F3SUJBZ0lJSjlXZmJjSVpYaWN3RFFZSktvWklodmNOQVFFTEJRQXdFakVRTUE0R0ExVUUKQXhNSGEzVmlaUzFqWVRBZUZ3MHlNVEEzTVRVeE5URTRNamhhRncwek1UQTNNVE14TlRNd01ERmFNQzR4RnpBVgpCZ05WQkFvVERuTjVjM1JsYlRwdFlYTjBaWEp6TVJNd0VRWURWUVFERXdwcmRXSmxMV0ZrYldsdU1JSUJJakFOCkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQXgzdElldjl4dHpoTVlmVG4zaFJBbXBnRys1RnMKOHlOUnQrK2IzMUpsM3R3KzkyaGdmeGwyTWc0cktVeWFyUkNkTGdwV0FiaHUyeDJTZUdTY0tWdGFoYVgyZ0xGMwpsVlVTVkhyWEZYQ2RSU1N4bnQ1eXQ0QUpwVlRMbGNPVVZtREtscEtvQi9VT1YrbGVKOFRydnJGWEU2ZWdBTzc1CnRKSkYxZURtbEVRR1F2WmxkRHM0RnNmeCtKelhhRXNpSTdySVM1MjJuUkdaa1dPaGZQU2lXYUVxRldlQU93MjIKMm5tNGVOS0VsMWtmNjlGL1pieHVVSDM3UDZmUEpQOG93QW44MG9EZFZOZm8yUWJTK29hZVMxK2hQNVJ2ZnErawozbDVlMGcrZ2c2ZnhxaWtrQXAySlNuRlJyYTNUdnRtRnBaeGo2NThDdE1xKzB0M3VqbDRNQk1CQ1JRSURBUUFCCm95Y3dKVEFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUhBd0l3RFFZSktvWkkKaHZjTkFRRUxCUUFEZ2dFQkFENUpkM3NMYmpORGZ5Z0kxclNnNWRZU2FHNmJ2NDN0OUdhbHR0MDhBZGZYVjNVcgpHY0lYaEZBTkwwMFZ2VmxLdDlXbCtYcWRxWnNRYWhmZTNISk85WHV4RDVscGczUEQ5T01SVGUvWGM4NDYxbTBWCkpDMjMyODYzaFRyaFZrUnByakJDb3hwVDZTOWVkM2kvWEFERVptWDJWTkhIUSt2TmJZeXVlc2ZRSWxpbFJ3R24KbStmK01VMmN0UGlvek1UbFBWaWthL3FvTWd3V09RMEFockhJc2dOMnJiTmQrRFh2YVVIMytjY292UGN5b0dlNApVNlJta2FJMEZ4cG5PN3d1bzIyaEFOeVpHU2t6eE11WkVQMVBGbERpdFY3aWNNYWZTekR4MUdTampRQXNvekR1CmREWFVwVUFPeHNFc1QzdkZtR3ZBNHhpTXBScHNDK3NCNWdqNkJwZz0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcEFJQkFBS0NBUUVBeDN0SWV2OXh0emhNWWZUbjNoUkFtcGdHKzVGczh5TlJ0KytiMzFKbDN0dys5MmhnCmZ4bDJNZzRyS1V5YXJSQ2RMZ3BXQWJodTJ4MlNlR1NjS1Z0YWhhWDJnTEYzbFZVU1ZIclhGWENkUlNTeG50NXkKdDRBSnBWVExsY09VVm1ES2xwS29CL1VPVitsZUo4VHJ2ckZYRTZlZ0FPNzV0SkpGMWVEbWxFUUdRdlpsZERzNApGc2Z4K0p6WGFFc2lJN3JJUzUyMm5SR1prV09oZlBTaVdhRXFGV2VBT3cyMjJubTRlTktFbDFrZjY5Ri9aYnh1ClVIMzdQNmZQSlA4b3dBbjgwb0RkVk5mbzJRYlMrb2FlUzEraFA1UnZmcStrM2w1ZTBnK2dnNmZ4cWlra0FwMkoKU25GUnJhM1R2dG1GcFp4ajY1OEN0TXErMHQzdWpsNE1CTUJDUlFJREFRQUJBb0lCQUJnT0h0UnVQMmxIeWJZNgpVVWV2aTRiWTlHYWJ4OWFlR0xta2xGaGUyRmdDbVRrK2hmeHR0cG9jcVVuR3FoUmFuNG13eDJSWHVFNkdCMmFyClEwV2RkWklPVEdhQ2dCZ3E5UlhvNWt6NGtvNkcrVUJlTk5rNkFHL0doUEpmYm1Eb05TWHBNNGdhSGd1dDRhUE0KRkYyZmh3K2d0Q1BJcmFYL3lab2NEOUlyVGRIL0s3Z0R4cHFkR2M3YUtmUXBvWHdjbWRFZGowL2JFMUhGZDlSUwpnZlpGcFp2RVNDcTlaQnluZVVWUHlTZVR5SlI0bWEzZEwzalJiWmZQTzlFcVNRbSsxbWZzYXhRU3k3K1JKKzY4Cmd2dGZCVVNGQ1l4N0JHemxiT1RHcHJ1em0vdGJXWHBrTCtxR1EwL3FHSllFd2dicFZ5YVo3WXV6N2RHT1VhdjcKSldBdzd4VUNnWUVBeTBkalV2NGliTGt4YjFlZkl0bE9uazZ3NFNlYzdtT1NNd3Y3c1dzSkpja0RkekRwMjMxNgpqRUg4dEEvTmswOEtRNS8vVDVFVGNmVnRqSWJhWmxRcDI0ZXAxOGdJUFJkN1RWbVgyN25FbkxBejJabzFMNUtwCmY0a0JOQUI3Y0J4M1JWYS81cHBJT0J0RDR6ekpwS1VQTFVFdGVUZ2VyOVVVTHVabkdQaWJCdWNDZ1lFQSt6ZkcKckorQjE2Z01rUmlmSGNmWU1qbVZwcXVTVFdncUVpaytjbUZ3VnVzL21IbGIxaDA2bFY0NUZWSG5tcm8zcWZVaQpQVXRDU29tWDYzZmlhWmwweG9rYXdVQUxZR1lTS1pxeTZFY2FJNEtTZ0NQaWtsS0wxbDd2cXFtbE5qV0N6dmdoCkVUaTQvbXZKMXBjUzQ5UytwSk9LRGJucFZDcWx5UXBRb2liY0EvTUNnWUFUcmppdWkwNDM2b0lmdm9MNHM4TkoKem1LUG1lODJvVXRCUi9LNVRaeVlIT3NKK2lGYUQ3N3luMXpnN2ZyQVBWSElGRkI2bXBnZ1cxdWMxRjJHdExWTQp2TWl6ekhrSHVTTkY3TnVuK1VkUXlEcHM0ZUl1VmV1MUhrV1FqRTluSGtwcDJ5ay9JVWJHcjlVVnhnZmJ1ZU5MClJWa3F1RVU0VHMvaWJvb2l2OGI2bHdLQmdRRGJHbWR1RVdSR2Vld1Q5Sng2ZGQxSzJNeDc1RElpenhHNmF6eHEKdUM4cHI5MzBsd3dRNzhjemxVMUdHZnhkQjhNYXVaRVdVbmhMMkR1bkJCVjFzb0NWMCtpQTJlSFNQdFBpYzJsTQppdzd5SDZTMG5CZTFOTWQvdmFkY2VyOThTeWwrYUEwM0h2akI5YkxCTlZ3bFYxeTYzMjlOejNNQWxIMnBuUlI4CmlGWG1Id0tCZ1FERFQycnU1RHRZU21PWTdzSzVwSFBvNVRja3B5K0hCWXJCRjVHaFQ2b2RWSHRhZW5KMG9mWS8KMHd0SkQ3VWlrU21zcmM0Y0h4ODQraXdvd0NyQVhXV2hDVDhQc2k5SHAwRUhVNWtSd3VPUWM0Z1RhQ3hvYytuOQp4UkJxMlFmS0NGeXhSQkZjY1ZaU3FDdENoWlQvaUMvZFBQMUJFNGR3RXdPYnBxdkxnRHJtVHc9PQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
```

### Add cluster and context

mac-pro 配置文 ~/.kube/config 内容如下：

```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN3akNDQWFxZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFTTVJBd0RnWURWUVFERXdkcmRXSmwKTFdOaE1CNFhEVEl4TURjeE5URXpOVEUxTVZvWERUTXhNRGN4TXpFek5URTFNVm93RWpFUU1BNEdBMVVFQXhNSAphM1ZpWlMxallUQ0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQ0FRb0NnZ0VCQU1PcFJVRzFaZm5NClcwc1pHamtBZ0dJcTg0UDlwTzh6RGxnc2RHUWJtQ0FYNUN0d3Mza0VXZzJVYnlYZUhhNDhxV09NRTVpNHpsZHEKMDl2QXZkeitoWHVjOHE0c0xqRjhFdW5jaEJhd002T1YrY04wbHlEOE0xcEUwelRoenRhYnZUQllhVVNuZmovbgpjditrWUlDNUdQRDRMdjFTWXBYOTdSK2R2TzdGaVg0a0t1d1p4ZVVETHdmQmN4NVdXaEdIT0tBQ0lFdHU5bkRyCkJTbnV2dE9lQ0kwUktrdzQwQ2pnMjVlYzVsT01paW1lNmpFdW5IZ0VpSkhmM0FtaGpSa0tmNVdaS2UreEpweDEKYjhIUFAvUXVJVnZSQVViOFA2VThUdGlmbVFRc0ZOMFZVK3h1QmN1b250UXFGVXFxQSt3MUtGUDBMOGVseHFIQgpESGc4elhhYXJDOENBd0VBQWFNak1DRXdEZ1lEVlIwUEFRSC9CQVFEQWdLa01BOEdBMVVkRXdFQi93UUZNQU1CCkFmOHdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBRk9ucGtjVmR5cW9JdUplZGNVWE9KK0Y3R0ViRkNCcytlcVkKLzBaMUZqNjQxZTJqZC9MNU9LMVJYTXF6ZEhIUm5WaEtUeXJDcWhXR2RLc2VjMmRrU1VBanh1TC9vQ1B1NldDMApaYkFPQXNCMXZuZW5WUTN0Y2h6OWU3ZnZ2b0dRWUV4NnpsMEVlcHA2N09EYUZIbHhsUGxINnN1dXhRM0VUQW9NCmV5UStBbHF0N0pwT3dzNEZRM3BBY1BOc2ZzZ0ZGQkJ0cjlPbDBMQm1xZUpBazlUN01LdHZSYnE2dkRsMWVTdFQKc05jMkdNaXpxUjY1QnQxc1B6QjF1VjdFditLVElFd1g3Vm84Um15ZjMrQjkzanBicHgrVEk1dGxxUXN6ZExUdgpod3pDQnhvZDJpcE9wdjU1Sm9ycmNsZ0RuOHFobTlYWVJXTk4vM2IzdGd2R1MvK1lKK1E9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://192.168.0.101:6443
  name: k8s-cluster1
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN3akNDQWFxZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFTTVJBd0RnWURWUVFERXdkcmRXSmwKTFdOaE1CNFhEVEl4TURjeE5URTFNVGd5T0ZvWERUTXhNRGN4TXpFMU1UZ3lPRm93RWpFUU1BNEdBMVVFQXhNSAphM1ZpWlMxallUQ0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQ0FRb0NnZ0VCQUs1WjdRSUNpM3dLCkhsbUZvYXJ1SVdqK2VwVnpkUjRtN2VsQnk3dGUxMWt0TzZ6VDRpbGZaODV3RDRlYzRSZmJGVDVwaDNJbDFCQkcKNnRhTXpSWEVoRFhGdHN5eWZhbEVOcVRETlV0SC8zaFZKZjZxbnk2SE1YV0hzdWlkZ3d1MXlYZG9Ka3dDbjVEbwowUjN1dEowTVBvenZoSzhOeHZJRk1xUjN4NjF0Y2RGUjF3RFVTeGlxeDdoQWtLQjBqUkkzSEJyR05QcDlwTTBtCjlnK1RWQm1WOUl2TkR0VUprNG5YWEVkbS9BOVJzQmNUWjVDVC9SbjQxN0NhbkwzdTJpTlU0UHVCUjZUMDB1bFAKbFRSRERwQ3Y1d1N0TWxLV3EzeHRiWE5Xa2JmU3dTUiswZ2M3WDR2WGVWS2hwdmNLL3FwbEtuSU1KcVZoc1ZINApHdTExTldBM05IRUNBd0VBQWFNak1DRXdEZ1lEVlIwUEFRSC9CQVFEQWdLa01BOEdBMVVkRXdFQi93UUZNQU1CCkFmOHdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBRWVHWUR2djM0bXZxNDRFUXRFdlBhM1V5V05iL0paOTUzWncKd1dId2d0S2dBd3RvbG5xdG9iMUJzdktBVE00VUEwbWNjVThpL0tmTFMvNVZxaC9vK0NGNjhnMmtEendnS2U3aApydWxOOTE2RWIwOS82M2NHYlhCV0xuT0JxNmRlT3NhcVN4dzNkYmtWN1pGQy9GS3IvOWNOYndmMXhRa1NvRDlXCjRtVnJPNzRMQlRHQk9OMFhxanllVmYwbnBMTlZZUzVsZEU1UHhaM21QZk5oOWptcWpVcjBJZ2ViZHJVZm54QU8KaHZEOHJGbE1QTUlaWEdkTjlZUHBxb2srVTY0SnA1NHhkNWNiYk5XaXdYYXRJYjV4dnoremZ5VFluYXJlUmtoKwpFd3Rtd3VZMitra1pkelpTdTFKSXBua0ZNTUhQRzI0b2k5RzBvekpsUDIwcE5iMFVHWUU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://192.168.0.102:6443
  name: k8s-cluster2
contexts:
- context:
    cluster: k8s-cluster1
    user: kube-admin-cluster1
  name: k8s-cluster1
- context:
    cluster: k8s-cluster2
    user: kube-admin-cluster2
  name: k8s-cluster2
current-context: k8s-cluster2
kind: Config
preferences: {}
users:
- name: kube-admin-cluster1
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM2VENDQWRHZ0F3SUJBZ0lJQ2RkVkJSRG9IM2t3RFFZSktvWklodmNOQVFFTEJRQXdFakVRTUE0R0ExVUUKQXhNSGEzVmlaUzFqWVRBZUZ3MHlNVEEzTVRVeE16VXhOVEZhRncwek1UQTNNVE14TkRFM016VmFNQzR4RnpBVgpCZ05WQkFvVERuTjVjM1JsYlRwdFlYTjBaWEp6TVJNd0VRWURWUVFERXdwcmRXSmxMV0ZrYldsdU1JSUJJakFOCkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQTJVYUpHMEN0VmhhS0hSeExURnFwbjlNaUcrUG8KdlZ6UGxZcXg0MXBCNk1DMmc1cHJ1MjBvdEwxWmxITkRFL01PQzNNNTVibjR0RDFzZUF5MjQ1ZEEzQUV6cml0UgovUEhNRzF3Ky9ZTTZiOTFQajd3cUd5UUE1dUNPTE1WbUYxQm5JbTRrSlNQUlNvRDFsZHMzcWFZeGl5VlpOT1VDClpXckR6NDh4Ry8wcG5PNDZNRGFNZ0VWS2VDU0ZhNm0zYjFaR1FWcEpqVi9HdVQ2QzhwOExucVBST0QzbkF3OXkKa1JnVm92MnlodGFwZXR6aDdVV2tTWHM3Vk5Gei9hM3pMT3FjQUdJa0plLzNXQ29iMTBPVG5Rbmg1Mms4SmphSgpzUm9JN2RLMURXMS9nT3crZDNKK2RkU0hYQTlreXF6UkZlWXJzaitRQTJHcFdab3RXbEJoWHVQWEJRSURBUUFCCm95Y3dKVEFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUhBd0l3RFFZSktvWkkKaHZjTkFRRUxCUUFEZ2dFQkFMejNNOWRxNzJvSENkSW16ODIzMXNuY0N6ZVI2QlFFQUhWOVlzR3RqSnl0Nm54UAo2bW1ORVE2eCtpSjhSenRHanVwb2Z2aGtwdS91VGZ0MUtYbm1yaHg5N1FQbWtqaXZSVnVoMGxjVE01aWVldXZSCmxONklqbzgwUVBuR2c5Q0tMWndONHZmTnBPbUg3a2J4VzJDOWJWVmRyb1VjQmZ3QmJ1ejFtQjNnVVVYYlovMlAKL3lsRStpTW5OQ0xseGtFYXMrZnpoL0VmTzVLRE8wY0xFMDJIaEV2WEI1WkFEZUViZzlRdHFMNkZwOW9pVTRYbgpXcTR5Z1llV2NLWndyZ0hWWXpaOXQ5RkdlQUNnM0FLWHdwcDhDN3lDSE1EUWpmcnBsQzI5QU1WN2RHWjZ4azI0CmxSU3JiRVA4NVF1M0tUOUZyS0NaY3E1OWd2bm0xUEREVHJLaVI4VT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcEFJQkFBS0NBUUVBMlVhSkcwQ3RWaGFLSFJ4TFRGcXBuOU1pRytQb3ZWelBsWXF4NDFwQjZNQzJnNXByCnUyMG90TDFabEhOREUvTU9DM001NWJuNHREMXNlQXkyNDVkQTNBRXpyaXRSL1BITUcxdysvWU02YjkxUGo3d3EKR3lRQTV1Q09MTVZtRjFCbkltNGtKU1BSU29EMWxkczNxYVl4aXlWWk5PVUNaV3JEejQ4eEcvMHBuTzQ2TURhTQpnRVZLZUNTRmE2bTNiMVpHUVZwSmpWL0d1VDZDOHA4TG5xUFJPRDNuQXc5eWtSZ1ZvdjJ5aHRhcGV0emg3VVdrClNYczdWTkZ6L2EzekxPcWNBR0lrSmUvM1dDb2IxME9UblFuaDUyazhKamFKc1JvSTdkSzFEVzEvZ093K2QzSisKZGRTSFhBOWt5cXpSRmVZcnNqK1FBMkdwV1pvdFdsQmhYdVBYQlFJREFRQUJBb0lCQUVXbDVxMWx2aXFxYnZ1Rgo1bDFEY3J4WTRjWXUrSnc2OUEvcnRibzdaSVZId1RuT2RscE9VNDRjWkdyQngrN05LdU5ndkY1M2p0RzRIdDBjCnRrT2VhSndkaG9OK1Azbmx5SmU4cWpSNXJISFBiNEdUdjZ1VGp2WnpaUi9VNXpUeUFSMTRVUDNXelhBa2hwVFQKQUxUUklYQ0pPRjlNU2NoWXdRdjN5clkrSU9pOG5WZWNTTzFQWEtURlN0QUFoQitiNzFUeEdNbituOVUzNkw2YgpWb2kzdnhOTHpvRUttNlZvV2FhanFzUm4xTEdEU0RVcm80LzF2Y2Y4clc4NHlSSGREb2U3d1l3dWFUV3VYc1NICk54OCt1UnpucExCTTN3OFFmNTgvNkZlN1dVMVZDL0J6Z0RhZkMzT0hlS3p5eWUwRTFCaTVuU2N5aFV4VWxES1QKTnFvNE1BRUNnWUVBK2EzYlo2REtkUkdabmo0cWY4NVlCNmtzbzJCc293Z2orNHRTbVJEQkpoV2M1b1BqTk5wNQp6QS9iNGtjUGc4b1hNZlRzNkEvN1FDQk0rSytnRmk3R211akVPVmQrb2tLeTdDNnpmZnVPWHB6ZWVmS1hKM3JZClczbHRNQks2TEYrUDJQc3ZyYmtYb2RtTUNGditRcjlnOWhFQkFydWxRaVp6SVhSVWJ6aVM4TUVDZ1lFQTNzYXMKb3VkZmFvRTYrQk50YktqOGdLNENsbkZMaVoyMCtQNWFiRVFDOEdsRmlabjMxV2NGUHFzbGdEWXhTL3lGQ0dLUAphcFdiNDlZRjRMMnl0YXhmUlhneXc0VWlHNFJRSXlVVDhJSFRXQTkwdFFxb3dBc3NQeHBUR1hTMWRQTXNJQUlGCkFDLzU1ZDVQV1hReVJqTSt6MzVmUEZzOHZRQ0l1TUNuYU90eXMwVUNnWUVBK1VTR2VHWUIybkRRMGpnMFM5YWcKOGowR3NMRnlwQzFiWnlYSU44S1BZc3RQRXFCM2RHdnVEem1DQjkxejh0b080RFFyVk4rbnNuVE5BN2FxOTVxSgpjMXlSa3NIMFRtQ1NxdE5SSmFUQWxWcTlqamdRaWp6TnhqMXJNZ1J3VkI2dnlTdTFoUlgyTHdLM0dCMW5zaEhJCjVzRkJKZzVheGJrSFZrNENnZXVVWDhFQ2dZQXA2b0hUQ091NEUyYXdCSi9ESVN5WlhhUlpBQ294VTM0WWwyc1cKRWRubnVEY0FRL3NRcVJpZ2lQMCtXWFAvRXgxSXpacWtlRS9qbDRKMW5kdkJPUlNYOHB6Q2t3c3UyRDluelhNcAovcE53YjBBTFRGMGgvVGd2QzFuMVlUTS9OUDNwYTlmYkNDdmg1MmxRc0g5QkhDVkdUMFhHQ25pc0t5eU9icGxSCk1YUGNiUUtCZ1FEcXg0ODhyc2krT0Jlci81MHNWZE1lTWNsSzFEaVZER013VFR3ZmZBRFFlT1BaN00xaitaU04KRVhYMHpGZGN4Mk81TU1hWkFNY01DMHl6Nm9HV0lVODRWT3AxWjNoOGV5dS9Ec3F0Y1ZIUkxDSmcrWWlVZkR6QgpuKzFXeEtkTmVUc1h6L01JMi9QNlQyQ2NSUHRyT2JScTBDUzdidDgzVzlqZmdsRm5CeStwc0E9PQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
- name: kube-admin-cluster2
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM2VENDQWRHZ0F3SUJBZ0lJSjlXZmJjSVpYaWN3RFFZSktvWklodmNOQVFFTEJRQXdFakVRTUE0R0ExVUUKQXhNSGEzVmlaUzFqWVRBZUZ3MHlNVEEzTVRVeE5URTRNamhhRncwek1UQTNNVE14TlRNd01ERmFNQzR4RnpBVgpCZ05WQkFvVERuTjVjM1JsYlRwdFlYTjBaWEp6TVJNd0VRWURWUVFERXdwcmRXSmxMV0ZrYldsdU1JSUJJakFOCkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQXgzdElldjl4dHpoTVlmVG4zaFJBbXBnRys1RnMKOHlOUnQrK2IzMUpsM3R3KzkyaGdmeGwyTWc0cktVeWFyUkNkTGdwV0FiaHUyeDJTZUdTY0tWdGFoYVgyZ0xGMwpsVlVTVkhyWEZYQ2RSU1N4bnQ1eXQ0QUpwVlRMbGNPVVZtREtscEtvQi9VT1YrbGVKOFRydnJGWEU2ZWdBTzc1CnRKSkYxZURtbEVRR1F2WmxkRHM0RnNmeCtKelhhRXNpSTdySVM1MjJuUkdaa1dPaGZQU2lXYUVxRldlQU93MjIKMm5tNGVOS0VsMWtmNjlGL1pieHVVSDM3UDZmUEpQOG93QW44MG9EZFZOZm8yUWJTK29hZVMxK2hQNVJ2ZnErawozbDVlMGcrZ2c2ZnhxaWtrQXAySlNuRlJyYTNUdnRtRnBaeGo2NThDdE1xKzB0M3VqbDRNQk1CQ1JRSURBUUFCCm95Y3dKVEFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUhBd0l3RFFZSktvWkkKaHZjTkFRRUxCUUFEZ2dFQkFENUpkM3NMYmpORGZ5Z0kxclNnNWRZU2FHNmJ2NDN0OUdhbHR0MDhBZGZYVjNVcgpHY0lYaEZBTkwwMFZ2VmxLdDlXbCtYcWRxWnNRYWhmZTNISk85WHV4RDVscGczUEQ5T01SVGUvWGM4NDYxbTBWCkpDMjMyODYzaFRyaFZrUnByakJDb3hwVDZTOWVkM2kvWEFERVptWDJWTkhIUSt2TmJZeXVlc2ZRSWxpbFJ3R24KbStmK01VMmN0UGlvek1UbFBWaWthL3FvTWd3V09RMEFockhJc2dOMnJiTmQrRFh2YVVIMytjY292UGN5b0dlNApVNlJta2FJMEZ4cG5PN3d1bzIyaEFOeVpHU2t6eE11WkVQMVBGbERpdFY3aWNNYWZTekR4MUdTampRQXNvekR1CmREWFVwVUFPeHNFc1QzdkZtR3ZBNHhpTXBScHNDK3NCNWdqNkJwZz0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    client-key-data: LS0tLS1CRUdJTiBSU0EgUFJJVkFURSBLRVktLS0tLQpNSUlFcEFJQkFBS0NBUUVBeDN0SWV2OXh0emhNWWZUbjNoUkFtcGdHKzVGczh5TlJ0KytiMzFKbDN0dys5MmhnCmZ4bDJNZzRyS1V5YXJSQ2RMZ3BXQWJodTJ4MlNlR1NjS1Z0YWhhWDJnTEYzbFZVU1ZIclhGWENkUlNTeG50NXkKdDRBSnBWVExsY09VVm1ES2xwS29CL1VPVitsZUo4VHJ2ckZYRTZlZ0FPNzV0SkpGMWVEbWxFUUdRdlpsZERzNApGc2Z4K0p6WGFFc2lJN3JJUzUyMm5SR1prV09oZlBTaVdhRXFGV2VBT3cyMjJubTRlTktFbDFrZjY5Ri9aYnh1ClVIMzdQNmZQSlA4b3dBbjgwb0RkVk5mbzJRYlMrb2FlUzEraFA1UnZmcStrM2w1ZTBnK2dnNmZ4cWlra0FwMkoKU25GUnJhM1R2dG1GcFp4ajY1OEN0TXErMHQzdWpsNE1CTUJDUlFJREFRQUJBb0lCQUJnT0h0UnVQMmxIeWJZNgpVVWV2aTRiWTlHYWJ4OWFlR0xta2xGaGUyRmdDbVRrK2hmeHR0cG9jcVVuR3FoUmFuNG13eDJSWHVFNkdCMmFyClEwV2RkWklPVEdhQ2dCZ3E5UlhvNWt6NGtvNkcrVUJlTk5rNkFHL0doUEpmYm1Eb05TWHBNNGdhSGd1dDRhUE0KRkYyZmh3K2d0Q1BJcmFYL3lab2NEOUlyVGRIL0s3Z0R4cHFkR2M3YUtmUXBvWHdjbWRFZGowL2JFMUhGZDlSUwpnZlpGcFp2RVNDcTlaQnluZVVWUHlTZVR5SlI0bWEzZEwzalJiWmZQTzlFcVNRbSsxbWZzYXhRU3k3K1JKKzY4Cmd2dGZCVVNGQ1l4N0JHemxiT1RHcHJ1em0vdGJXWHBrTCtxR1EwL3FHSllFd2dicFZ5YVo3WXV6N2RHT1VhdjcKSldBdzd4VUNnWUVBeTBkalV2NGliTGt4YjFlZkl0bE9uazZ3NFNlYzdtT1NNd3Y3c1dzSkpja0RkekRwMjMxNgpqRUg4dEEvTmswOEtRNS8vVDVFVGNmVnRqSWJhWmxRcDI0ZXAxOGdJUFJkN1RWbVgyN25FbkxBejJabzFMNUtwCmY0a0JOQUI3Y0J4M1JWYS81cHBJT0J0RDR6ekpwS1VQTFVFdGVUZ2VyOVVVTHVabkdQaWJCdWNDZ1lFQSt6ZkcKckorQjE2Z01rUmlmSGNmWU1qbVZwcXVTVFdncUVpaytjbUZ3VnVzL21IbGIxaDA2bFY0NUZWSG5tcm8zcWZVaQpQVXRDU29tWDYzZmlhWmwweG9rYXdVQUxZR1lTS1pxeTZFY2FJNEtTZ0NQaWtsS0wxbDd2cXFtbE5qV0N6dmdoCkVUaTQvbXZKMXBjUzQ5UytwSk9LRGJucFZDcWx5UXBRb2liY0EvTUNnWUFUcmppdWkwNDM2b0lmdm9MNHM4TkoKem1LUG1lODJvVXRCUi9LNVRaeVlIT3NKK2lGYUQ3N3luMXpnN2ZyQVBWSElGRkI2bXBnZ1cxdWMxRjJHdExWTQp2TWl6ekhrSHVTTkY3TnVuK1VkUXlEcHM0ZUl1VmV1MUhrV1FqRTluSGtwcDJ5ay9JVWJHcjlVVnhnZmJ1ZU5MClJWa3F1RVU0VHMvaWJvb2l2OGI2bHdLQmdRRGJHbWR1RVdSR2Vld1Q5Sng2ZGQxSzJNeDc1RElpenhHNmF6eHEKdUM4cHI5MzBsd3dRNzhjemxVMUdHZnhkQjhNYXVaRVdVbmhMMkR1bkJCVjFzb0NWMCtpQTJlSFNQdFBpYzJsTQppdzd5SDZTMG5CZTFOTWQvdmFkY2VyOThTeWwrYUEwM0h2akI5YkxCTlZ3bFYxeTYzMjlOejNNQWxIMnBuUlI4CmlGWG1Id0tCZ1FERFQycnU1RHRZU21PWTdzSzVwSFBvNVRja3B5K0hCWXJCRjVHaFQ2b2RWSHRhZW5KMG9mWS8KMHd0SkQ3VWlrU21zcmM0Y0h4ODQraXdvd0NyQVhXV2hDVDhQc2k5SHAwRUhVNWtSd3VPUWM0Z1RhQ3hvYytuOQp4UkJxMlFmS0NGeXhSQkZjY1ZaU3FDdENoWlQvaUMvZFBQMUJFNGR3RXdPYnBxdkxnRHJtVHc9PQotLS0tLUVORCBSU0EgUFJJVkFURSBLRVktLS0tLQo=
```

### 演示：设置 context

```bash
# 1. 查看当前的 cluster 和 context
> kubectl config get-contexts
CURRENT   NAME           CLUSTER        AUTHINFO              NAMESPACE
*         k8s-cluster1   k8s-cluster1   kube-admin-cluster1
          k8s-cluster2   k8s-cluster2   kube-admin-cluster2

# 2. 查看当前 context 中的 cluster 中的 节点资源
> kubectl get nodes
NAME            STATUS   ROLES                      AGE   VERSION
192.168.0.101   Ready    controlplane,etcd,worker   17h   v1.20.8

# 3. 切换 context 为 k8s-cluster2
kubectl config use-context k8s-cluster2
Switched to context "k8s-cluster2".

# 4. 再次查看当前的 cluster 和 context
> kubectl config get-contexts
CURRENT   NAME           CLUSTER        AUTHINFO              NAMESPACE
          k8s-cluster1   k8s-cluster1   kube-admin-cluster1
*         k8s-cluster2   k8s-cluster2   kube-admin-cluster2

# 5. 查看当前 context 中的 cluster 中的 节点资源
> kubectl get nodes
NAME            STATUS   ROLES                      AGE   VERSION
192.168.0.102   Ready    controlplane,etcd,worker   16h   v1.20.8
```

## namespace

### 定义 namespace

2.1 create-pod-with-namespace.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: demo
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

### 演示：创建 namespace

```bash
# 1. 获取当前 k8s 中的 namespace
> kubectl get Namespace
NAME              STATUS   AGE
default           Active   16h
ingress-nginx     Active   16h
kube-node-lease   Active   16h
kube-public       Active   16h
kube-system       Active   16h

# 2. 创建 namespace demo
> kubectl create namespace demo

# 3. create pod with namespace
> kubectl create -f "2.1 create-pod-with-namespace.yaml"

# 4. 根据 namespace 过滤 pod
> kubectl get pod --namespace demo                                                             NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          61s

# 5. 删除 namespace demo
> kubectl delete namespace demo
namespace "demo" deleted
```

## Pod

### 定义 pod

3.1 pod definition.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-busybox
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
  - name: busybox
    image: busybox
    command: ["/bin/sh"]
    args: ["-c","while true;do echo hello;sleep 10;done"]
```

### 演示：创建 pod

```bash
# 1. 根据 yaml 创建 pod
> kubectl create -f "3.1 pod definition.yaml"
pod/nginx-busybox created

# 2. 获取当前 k8s 中的 pod
> kubectl get pods
NAME            READY   STATUS    RESTARTS   AGE
nginx-busybox   2/2     Running   0          112s

# 3. 获取 pod 的详细信息
> kubectl describe pod nginx-busybox
Name:         nginx-busybox
Namespace:    default
Priority:     0
Node:         192.168.0.102/192.168.0.102
Start Time:   Fri, 16 Jul 2021 17:07:26 +0800
Labels:       <none>
Annotations:  cni.projectcalico.org/podIP: 10.42.0.13/32
              cni.projectcalico.org/podIPs: 10.42.0.13/32
Status:       Running
IP:           10.42.0.13
IPs:
  IP:  10.42.0.13
Containers:
  nginx:
    Container ID:   docker://2faf5c6ca9a8693b3d79a74aceb428e95ab3eab8ff08d5c3e2dbb5b0cba4fb0a
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:353c20f74d9b6aee359f30e8e4f69c3d7eaea2f610681c4a95849a2fd7c497f9
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Fri, 16 Jul 2021 17:07:44 +0800
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-z429d (ro)
  busybox:
    Container ID:  docker://40fb9f0aad6828f12a64f3b5ac54f481808a45d759359a85ff1fa9f1f66f5281
    Image:         busybox
    Image ID:      docker-pullable://busybox@sha256:0f354ec1728d9ff32edcd7d1b8bbdfc798277ad36120dc3dc683be44524c8b60
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/sh
    Args:
      -c
      while true;do echo hello;sleep 10;done
    State:          Running
      Started:      Fri, 16 Jul 2021 17:08:03 +0800
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-z429d (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-z429d:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-z429d
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                 node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  3m51s  default-scheduler  Successfully assigned default/nginx-busybox to 192.168.0.102
  Normal  Pulling    3m50s  kubelet            Pulling image "nginx"
  Normal  Pulled     3m33s  kubelet            Successfully pulled image "nginx" in 16.825562979s
  Normal  Created    3m33s  kubelet            Created container nginx
  Normal  Started    3m33s  kubelet            Started container nginx
  Normal  Pulling    3m33s  kubelet            Pulling image "busybox"
  Normal  Pulled     3m14s  kubelet            Successfully pulled image "busybox" in 18.599300936s
  Normal  Created    3m14s  kubelet            Created container busybox
  Normal  Started    3m14s  kubelet            Started container busybox

# 4. 按指定格式输出 pod 信息，-o 可选参数：wide、json、yaml
> kubectl get pods nginx-busybox -o wide
NAME            READY   STATUS    RESTARTS   AGE     IP           NODE            NOMINATED NODE   READINESS GATES
nginx-busybox   2/2     Running   0          5m57s   10.42.0.13   192.168.0.102   <none>           <none>

# 5. 进入某个 pod 容器内部
## 注意：如果一个pod中有多个容器，默认是进第一个容器。如果想进入其它容器，可以通过 -c 参数指定
> kubectl exec nginx-busybox -it sh
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
Defaulting container name to nginx.
Use 'kubectl describe pod/nginx-busybox -n default' to see all of the containers in this pod.
#

# 6. 在 pod 中执行 linux 命令(date)
kubectl exec nginx-busybox -- date
Defaulting container name to nginx.
Use 'kubectl describe pod/nginx-busybox -n default' to see all of the containers in this pod.
Fri Jul 16 09:27:17 UTC 2021

# 7. 在第二个容器（busybox）中执行 linux 命令(date)
> kubectl exec nginx-busybox -c busybox -- date
Fri Jul 16 09:28:04 UTC 2021

# 8. 根据 yaml 删除 pod
> kubectl delete -f "3.1 pod definition.yaml"
pod "nginx-busybox" deleted
```

## deployment

### 4.1 nginx_deploymdnet.yml

```yaml
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template: # create pods using pod definition in this template
    metadata:
      # unlike pod-nginx.yaml, the name is not included in the meta data as a unique name is
      # generated from the deployment name
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

### 4.2 nginx_deployment_update.yml

```yaml
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.8 # Update the version of nginx from 1.7.9 to 1.8
        ports:
        - containerPort: 80
```

### 4.3 nginx_deployment_scale.yml

```yaml
apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 4 # Update the replicas from 2 to 4
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.8
        ports:
        - containerPort: 80
```

### 演示：创建 deployment

```yaml
# 1. 创建 deployment
> kubectl create -f "4.1 nginx_deploymdnet.yml"
deployment.apps/nginx-deployment created

# 2. 查看当前 k8s 中的 pod
> kubectl get pod
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-5d59d67564-4whs2   1/1     Running   0          3m32s
nginx-deployment-5d59d67564-j9p9b   1/1     Running   0          3m32s

# 3. 根据标签 nginx 筛选 pod
kubectl get pod -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-5d59d67564-4whs2   1/1     Running   0          3m59s
nginx-deployment-5d59d67564-j9p9b   1/1     Running   0          3m59s

# 4. 获取 deployment（nginx-deployment）的信息，按照 wide 模式输出
> kubectl get deployment nginx-deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES        SELECTOR
nginx-deployment   2/2     2            2           5m10s   nginx        nginx:1.7.9   app=nginx

# 5. 演示：deployment 自动维护 pod 的数量
## 5.1 手动删除 pod nginx-deployment-5d59d67564-4whs2，并
> kubectl delete pod nginx-deployment-5d59d67564-4whs2
pod "nginx-deployment-5d59d67564-4whs2" deleted
## 5.2 观察 pod 的状态，说明 deployment 会自动维护 pod 的数量
> kubectl get pod -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-5d59d67564-j9p9b   1/1     Running   0          9m15s
nginx-deployment-5d59d67564-k8bbt   1/1     Running   0          38s

# 6. 更新 nginx版本（从1.7.9 到 1.8）
> kubectl apply -f "4.2 nginx_deployment_update.yml"
Warning: resource deployments/nginx-deployment is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
deployment.apps/nginx-deployment configured
> kubectl get deployment nginx-deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES      SELECTOR
nginx-deployment   2/2     1            2           15m   nginx        nginx:1.8   app=nginx

# 7. 伸缩 pod 数量
> kubectl apply -f "4.3 nginx_deployment_scale.yml"
deployment.apps/nginx-deployment configured
> kubectl get pod -l app=nginx
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-64c9d67564-6mclw   1/1     Running   0          15s
nginx-deployment-64c9d67564-8ch7n   1/1     Running   0          113s
nginx-deployment-64c9d67564-db7mv   1/1     Running   0          15s
nginx-deployment-64c9d67564-ffhs6   1/1     Running   0          2m45s

# 8. 通过 vim 更新 deployment(修改pod数量为3)
> kubectl edit deployment nginx-deployment

# 9. 通过 kubectl 命令伸缩 deployment（将 pod 数量从 3 变为 4）
> kubectl scale --current-replicas=3 --replicas=4 deployment/nginx-deployment
deployment.apps/nginx-deployment scaled
> kubectl get deployment nginx-deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES      SELECTOR
nginx-deployment   4/4     4            4           30m   nginx        nginx:1.8   app=nginx

# 10. 通过命令行更新 deployment 中 nginx 的 image 版本（从1.8变为1.7.9）
> kubectl set image deployment/nginx-deployment nginx=1.7.9
deployment.apps/nginx-deployment image updated
> kubectl get deployment nginx-deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES   SELECTOR
nginx-deployment   4/4     3            4           34m   nginx        1.7.9    app=nginx

# 11. 获取 replilcaset
> kubectl get replicaset
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-64c9d67564   4         4         4       7s

# 12. 获取 replicaset 的更新状态
> kubectl set image deployment/nginx-deployment nginx=1.7.9
deployment.apps/nginx-deployment image updated
> kubectl rollout status deployment nginx-deployment

# 13. 查看 deployment 的更新历史及版本
> kubectl rollout history deployment nginx-deployment
deployment.apps/nginx-deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
3         <none>

# 14. 回滚 deployment 的到特定版本
> kubectl rollout history deployment nginx-deployment --revision 2
deployment.apps/nginx-deployment with revision #2
Pod Template:
  Labels:	app=nginx
	pod-template-hash=64c9d67564
  Containers:
   nginx:
    Image:	nginx:1.8
    Port:	80/TCP
    Host Port:	0/TCP
    Environment:	<none>
    Mounts:	<none>
  Volumes:	<none>
> kubectl rollout history deployment nginx-deployment --revision 3
deployment.apps/nginx-deployment with revision #3
Pod Template:
  Labels:	app=nginx
	pod-template-hash=5dd569b986
  Containers:
   nginx:
    Image:	1.7.9
    Port:	80/TCP
    Host Port:	0/TCP
    Environment:	<none>
    Mounts:	<none>
  Volumes:	<none>

# 15. 回滚 deployment 的到上一版本
> kubectl rollout undo deployment nginx-deployment
deployment.apps/nginx-deployment rolled back

# 16. 删除 deployment
> kubectl delete deployment nginx-deployment
deployment.apps "nginx-deployment" deleted
```

## Service

### Service 介绍

由于一些原因，导致 pod 不方便提供服务，比如：

- pod 的数量可能随时会增加/减少
- pod 的ip地址随时可能会发生变化

因此，需要使用 Servce，通过 label 筛选，将抽象的一组 pod 组织起来，对外提供服务。

### Service 类型

- ClusterIP(默认)
- NodePort
- LoadBalancer

| 对比项 | ClusterIP | NodePort | LoadBalancer |
| ---- |----|----| ----|
| 是否默认 | 是 | 否 | 否 |
| 集群内任意节点可访问 | 是 |  |  |
| 实现原理 | 基于iptables的链 | 在所有节点（虚拟机）上开放一个特定端口，任何发送到该端口的流量都被转发到对应服务。 | 端口转发 |
| 应用场景 | 集群内访问 | 开发调试 | 云厂商环境/生产环境 |

### 5.0.1 pod.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

### 5.0.2 busybox.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-busybox
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
```

### 5.1 ClusterIP.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-nginx
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

### 5.2 NodePort.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-nginx
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

### 演示：Service

#### 演示：创建 ClusterIP 类型的 Service

```bash
# 1. 准备工作：创建pod
> kubectl create -f "5.0.1 pod.yaml"
pod/pod-nginx created

# 2. 创建 ClusterIP 类型的 Service
> kubectl create -f "5.1 ClusterIP.yaml"
service/service-nginx created

# 3. 获取 Service 列表
> kubectl get svc
NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
kubernetes      ClusterIP   10.43.0.1      <none>        443/TCP    3d16h
service-nginx   ClusterIP   10.43.73.249   <none>        8080/TCP   18s

# 3. 根据 Service 的 ClusterIP 和  port 访问 Service
> curl 10.43.73.249:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

# 4. 删除 Service
## 4.1 方法一：根据 yaml 删除 Service
> kubectl delete -f "5.1 ClusterIP.yaml"
> service "service-nginx" deleted
## 4.2 方法二：使用命令删除 Service
> kubectl delete svc service-nginx
service "service-nginx" deleted

# 5. 删除 pod
## 5.1 方法一：根据 yaml 删除 pod
> kubectl delete -f "5.0.1 pod.yaml"
pod "pod-nginx" deleted
## 5.2 方法二：使用命令行删除 pod
> kubectl get pod
NAME        READY   STATUS    RESTARTS   AGE
pod-nginx   1/1     Running   0          15m
> kubectl delete pod pod-nginx
pod "pod-nginx" deleted
```

#### 演示：创建 NodePort 类型的 Service

```bash
# 1. 准备工作：创建pod
> kubectl create -f "5.0.1 pod.yaml"
pod/pod-nginx created

# 2. 创建 NodePort 类型的 Service
> kubectl create -f "5.2 NodePort.yaml"
service/service-nginx created

# 3. 获取 Service 列表
> kubectl get svc
NAME            TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
kubernetes      ClusterIP   10.43.0.1     <none>        443/TCP          3d16h
service-nginx   NodePort    10.43.36.91   <none>        8080:32008/TCP   22s

# 4. 使用 任意 Node 的IP 和 转发端口（32008）访问 Service
> curl 192.168.0.101:32008
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

# 4. 删除 Service
## 4.1 方法一：根据 yaml 删除 Service
> kubectl delete -f "5.1 ClusterIP.yaml"
> service "service-nginx" deleted
## 4.2 方法二：使用命令删除 Service
> kubectl delete svc service-nginx
service "service-nginx" deleted

# 5. 删除 pod
## 5.1 方法一：根据 yaml 删除 pod
> kubectl delete -f "5.0.1 pod.yaml"
pod "pod-nginx" deleted
## 5.2 方法二：使用命令行删除 pod
> kubectl get pod
NAME        READY   STATUS    RESTARTS   AGE
pod-nginx   1/1     Running   0          15m
> kubectl delete pod pod-nginx
pod "pod-nginx" deleted
```

#### 演示：创建 LoadBalancer 类型的 Service

```bash
# 1. 将 pod 的 type 更改为 LoadBalancer
> kubectl expose pod nginx-pod --type=LoadBalancer
service "nginx-pod" exposed

# 2. 通过 DNS Name 访问 LoadBalancer 类型的 Service
> curl "DNS Name"
```

### 演示：Service Auto Discovery

#### 演示：检查 k8s 环境是否支持 Service AutoDiscovery

```bash
# 检查是否存在 coredns 或 kubedns，如果不存在，则不支持 Service Auto Discovery，需要手动安装
> kubectl get pod -o wide -n kube-system                                   ─╯
NAME                                       READY   STATUS      RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
calico-kube-controllers-7d5d95c8c9-hhwnq   1/1     Running     2          3d17h   10.42.0.15      192.168.0.101   <none>           <none>
canal-sn6f8                                2/2     Running     4          3d17h   192.168.0.101   192.168.0.101   <none>           <none>
coredns-55b58f978-7qc92                    1/1     Running     2          3d17h   10.42.0.12      192.168.0.101   <none>           <none>
coredns-autoscaler-76f8869cc9-2pmch        1/1     Running     2          3d17h   10.42.0.16      192.168.0.101   <none>           <none>
metrics-server-55fdd84cd4-64tqc            1/1     Running     2          3d17h   10.42.0.13      192.168.0.101   <none>           <none>
rke-coredns-addon-deploy-job-cmt88         0/1     Completed   0          3d17h   192.168.0.101   192.168.0.101   <none>           <none>
rke-ingress-controller-deploy-job-tpg8q    0/1     Completed   0          3d17h   192.168.0.101   192.168.0.101   <none>           <none>
rke-metrics-addon-deploy-job-j9j6s         0/1     Completed   0          3d17h   192.168.0.101   192.168.0.101   <none>           <none>
rke-network-plugin-deploy-job-6rrjk        0/1     Completed   0          3d17h   192.168.0.101   192.168.0.101   <none>           <none>
```

#### 演示：基于 DNS 实现 Service Auto Discovery

```bash
# 1. 环境准备
## 1.1 创建 pod nginx
> kubectl create -f "5.0.1 pod.yaml"
> pod/pod-nginx created
## 1.2 创建 pod busybox
> kubectl create -f "5.0.2 busybox.yaml"
> pod/pod-busybox created
## 1.3 创建 service
> kubectl expose pod pod-nginx --name service-nginx
service/service-nginx exposed
## 1.4 查看 service 列表及 Service 对应的 ip地址
> kubectl get svc
NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes      ClusterIP   10.43.0.1      <none>        443/TCP   3d19h
service-nginx   ClusterIP   10.43.203.20   <none>        80/TCP    64s

# 2. 演示 基于 DNS 实现 Service Auto Discovery
## 2.1 获取 pod 列表
> kubectl get pod -o wide
NAME          READY   STATUS    RESTARTS   AGE   IP           NODE            NOMINATED NODE   READINESS GATES
pod-busybox   1/1     Running   0          27s   10.42.0.21   192.168.0.101   <none>           <none>
pod-nginx     1/1     Running   0          11m   10.42.0.19   192.168.0.101   <none>           <none>

## 2.2 进入 pod busybox 内部
> kubectl exec -it pod-busybox -- sh

## 2.3 查看容器的ip地址
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
3: eth0@if16: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1450 qdisc noqueue
    link/ether 86:fe:52:2b:9e:ef brd ff:ff:ff:ff:ff:ff
    inet 10.42.0.21/32 brd 10.42.0.21 scope global eth0
       valid_lft forever preferred_lft forever

## 2.4 测试 到 pod-nginx(10.42.0.19) 网络联通性
/ # ping 10.42.0.19
PING 10.42.0.19 (10.42.0.19): 56 data bytes
64 bytes from 10.42.0.19: seq=0 ttl=63 time=0.324 ms
64 bytes from 10.42.0.19: seq=1 ttl=63 time=0.108 ms
^C
--- 10.42.0.19 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.085/0.172/0.324 ms

## 2.5 查看 dns server的 ip 地址
/ # more /etc/resolv.conf
nameserver 10.43.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5

## 2.6 通过 ping 获取 service-nginx 的 ip地址
/ # ping service-nginx(可以解析出 service-nginx 对应的 ip 地址为 10.43.203.20)
PING service-nginx (10.43.203.20): 56 data bytes
^C
--- service-nginx ping statistics ---
19 packets transmitted, 0 packets received, 100% packet loss

## 2.7 通过 nslookup 命令 获取 service-nginx 的 ip 地址
/ # nslookup service-nginx
nslookup service-nginx
Server:		10.43.0.10
Address:	10.43.0.10:53

Name:	service-nginx.default.svc.cluster.local
Address: 10.43.203.20


# 3. 获取 kube-dns 的 ip 地址
> kubectl get svc -n kube-system
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                  AGE
kube-dns         ClusterIP   10.43.0.10     <none>        53/UDP,53/TCP,9153/TCP   3d19h
metrics-server   ClusterIP   10.43.70.165   <none>        443/TCP                  3d19h
## 注意：这里获取到的 kube-dns 的 ip 地址是 10.43.0.10，与上一步在 busybox pod中获取到的 dns server 的 ip 地址相同

# 4. 清理演示环境
## 4.1 删除 service service-nginx
> kubectl delete svc service-nginx
service "service-nginx" deleted
## 4.2 删除 pod pod-nginx
> kubectl delete pod pod-nginx
pod "pod-nginx" deleted
## 4.3 删除 pod pod-bysybox
> kubectl delete pod pod-busybox
pod "pod-busybox" deleted
```

#### 演示：基于 环境变量 实现 Service Auto Discovery

```bash
# 1. 环境准备（注意：顺序很重要，busybox必须最后创建）
## 1.1 创建 pod pod-nginx
> kubectl create -f "5.0.1 pod.yaml"
pod/pod-nginx created
## 1.2 创建 service service-nginx
> kubectl create -f "5.1 ClusterIP.yaml"
service/service-nginx created
## 1.3 创建 pod pod-busybox
> kubectl create -f "5.0.2 busybox.yaml"
pod/pod-busybox created

# 2. 输出 pod pod-busybox 中的环境变量(可以得到 service-nginx有关的环境变量)
> kubectl exec pod-busybox -- env                                           
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=pod-busybox
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT_443_TCP=tcp://10.43.0.1:443
KUBERNETES_PORT_443_TCP_ADDR=10.43.0.1
SERVICE_NGINX_PORT_8080_TCP=tcp://10.43.167.52:8080
SERVICE_NGINX_PORT_8080_TCP_PORT=8080
SERVICE_NGINX_PORT_8080_TCP_ADDR=10.43.167.52
KUBERNETES_SERVICE_HOST=10.43.0.1
SERVICE_NGINX_SERVICE_HOST=10.43.167.52
SERVICE_NGINX_PORT_8080_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT=tcp://10.43.0.1:443
SERVICE_NGINX_SERVICE_PORT=8080
SERVICE_NGINX_PORT=tcp://10.43.167.52:8080
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP_PORT=443
HOME=/root

# 3. 清理演示环境
## 3.1 删除 service service-nginx
> kubectl delete svc service-nginx

service "service-nginx" deleted
## 3.2 删除 pod pod-nginx
> kubectl delete pod pod-nginx

pod "pod-nginx" deleted
## 3.3 删除 pod pod-busybox
> kubectl delete pod pod-busybox
pod "pod-busybox" deleted
```

## Health Check

### Health Check 介绍

健康检查通过探针的方式，可以检测 pod 的健康状态，当 pod 状态不健康时，避免把请求转发给不健康的 pod。

### 探针支持的类型

探针按照方式支持三种类型，分别是：

- HTTP
- Command
- TCP

### HTTP 方式探针示例

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    prot: 8080
    httpHeaders:
    - name: X-Custom-Header
      value: Awesome
  initialDelaySeconds: 3
  periodSeconds: 3
```

### Command 方式探针示例

```yaml
livenessProbe:
  exec:
    command:
    - cat
    - /tmp.healthy
  initialDelaySeconds: 5
  periodSeconds: 5
```

### TCP 方式探针示例

```yaml
livenessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 15
  periodSeconds: 20
```

### Health Check 中两种探针的对比

| 对比项 | Liveness Probe | readiness Probe |
| ---- |----|-----|
| 配置和参数 | 相同 | 相同 |
| 探测失败后的行为 | 重启容器 | 把容器标记为 Unready，不接受请求 |
| 依赖性 | 而至是相互独立，没有依赖，既可以独立使用，也可以同时使用 | 同 Liveness Probe |
| 作用 | 判断是否需要重启以实现自愈 | 判断容器是否准备好对外提供服务 |
| 初始值 | 成功，防止应用在没成功启动前，被误杀 | 失败，防止应用还没准备好，有请求进来 |
| 默认值 | 二者没有配置的话，默认状态都是成功 | - |
| 返回值 | 返回值在[200,400]范围内认为成功，返回值 5xx认为失败 | 同 Liveness Probe |

- 二者不能相互替代，根据实际情况，配合使用。
- 只配置了 readiness 是无法出发容器重启的。
- 只配置了 liveness，可能应用还没准备好，导致请求失败，status 是 running，Ready 是 0/1。

### Liveness Probe 配置示例

```yaml
livenessProbe:
  enabled: true
  httpGet:
  port: 8080
  scheme: HTTP
  initialDelaySeconds: 60   # 表示延迟30S开始第一次探测，默认值是0，最小值是0
  timeoutSeconds: 35        # 表示每次探测的超时时间，35S后如果没返回结果就认为超时失败，默认值是1，最小值是1
  periodSeconds: 30         # 表示多久进行一次探测，默认是10S，最小值是1
  successThreshold: 1       # 表示在探测失败后，最小的连续成功被认为是成功的，默认值是1，最小值是1
  failureThreshold: 3       # 表示当探测失败时，Kubernetes将在认为失败前尝试failureThreshold次数。默认值是3，最小值是1;Liveness认为失败的操作是重启pod，而readiness认为失败的操作是把pod标记为 Unready
```

### readness probe 配置示例

```yaml
readinessProbe:
  enabled: true
  httpGet:
  port: 8080
  scheme: HTTP
  initialDelaySeconds: 30   # 表示延迟30S开始第一次探测，默认值是0，最小值是0
  timeoutSeconds: 35        # 表示每次探测的超时时间，35S后如果没返回结果就认为超时失败，默认值是1，最小值是1
  periodSeconds: 30         # 表示多久进行一次探测，默认是10S，最小值是1
  successThreshold: 1       # 表示在探测失败后，最小的连续成功被认为是成功的，默认值是1，最小值是1
  failureThreshold: 3       # 表示当探测失败时，Kubernetes将在认为失败前尝试failureThreshold次数。默认值是3，最小值是1;Liveness认为失败的操作是重启pod，而readiness认为失败的操作是把pod标记为 Unready
```

## Ingress

### Ingress Resource

#### Name based routing

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: go-app-ingress
  namespace: ingress-nginx
spec:
  rules:
  - host: demo.infracloud.space
    http:
      paths:
      - backend:
        serviceName: demo-go-app-svc
        servicePort: 80
```

#### Path based routing

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: go-app-ingress
  namespace: ingress-nginx
spec:
  rules:
  - host: demo.infracloud.space
    http:
      paths:
      - path: /prod
        backend:
          serviceName: demo-go-app-svc
          servicePort: 80
      - path: /canary
        backend:
          serviceName: demo-go-app-canary
          servicePort: 80
```

### Ingress Controller

通用的 Ingress Controller：

- Nginx
- Traefik
- HAproxy
- Envoy

## Volumes

### hostPath

#### 定义 hostPath

8.1 hostPath.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - name: busybox1
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    volumeMounts:
    - mountPath: /test-pd
      name: test-volume
  - name: busybox2
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    volumeMounts:
    - mountPath: /test-pd
      name: test-volume
  volumes:
  - name: test-volume
    hostPath:
      # directory location on host
      path: /data
      # this field is optional
      type: DirectoryOrCreate
```

#### 演示：创建 hostPath

```bash
# 1. 准备环境
> mkdir -p /data

# 2. 创建 pod
> kubectl create -f "8.1 hostPath.yaml"
pod/test-pd created

# 3. 获取 pod 列表
> kubectl get pod -o wide
NAME      READY   STATUS    RESTARTS   AGE   IP           NODE            NOMINATED NODE   READINESS GATES
test-pd   2/2     Running   0          44s   10.42.0.25   192.168.0.101   <none>           <none>

# 4. 演示 hostPath
## 4.1 从 /data 创建文件
> cd /data
> echo "test0 from /data" >> test
## 4.2 从 pod busybox1 创建文件
> kubectl exec -it test-pd -- sh
Defaulted container "busybox1" out of: busybox1, busybox2
/ # cd /test-pd/
/test-pd # ls
test
/test-pd # echo "test1 from busybox1" >> test
/test-pd # exit
## 4.3 从 pod busybox2 创建文件
> kubectl exec -it test-pd -c busybox2 -- sh
/ # cd /test-pd
/test-pd # echo "test2 from busybox2" >> test
/test-pd # exit
## 4.4 从 /data 查看测试文件
> cd /data
> more test
test0 from /data
test1 from busybox1
test2 from busybox2

# 5. 删除演示环境
> kubectl delete pod test-pd
pod "test-pd" deleted
```

### PVC & PV

`PVC`是一个用户请求，用于向 Kubernetes 申请存储资源。Kubernetes收到申请以后，会由 Storage.Class 自动分配 `PV`

#### 8.2.1 pvc.yaml

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: hello-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi
```

#### 8.2.2 pvc-mysql.yaml

```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mysql-volumeclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi
```

#### 8.2.3 mysql.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - image: mysql:5.6
          name: mysql
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: password
          ports:
            - containerPort: 3306
              name: mysql
          volumeMounts:
            - name: mysql-persistent-storage
              mountPath: /var/lib/mysql
      volumes:
        - name: mysql-persistent-storage
          persistentVolumeClaim:
            claimName: mysql-volumeclaim
```

#### 演示：创建pvc & pv

```bash
# 1. 创建 pvc
> kubectl create -f "8.2.1 pvc.yaml"
persistentvolumeclaim/hello-pvc created
# 2. 获取 pvc 列表(本次实验环境由于没有配置 Storage.Class，所以pvc一直是pending状态，如果配置 Storage.Class，则正常应该是 Bound 状态)
> kubectl get pvc
NAME        STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
hello-pvc   Pending                                                     73s
# 3. 获取 pv(由于上一步的pvc一直是pending状态，所以pv就无法正常分配)
> kubectl get pv
No resources found
# 4. 清理演示环境(删除pvc，所有相应的pv也会被删除)
> kubectl delete pvc hello-pvc
persistentvolumeclaim "hello-pvc" deleted
```

####  演示：mysql使用pvc

```bash
# 1. 创建 mysql 的pvc
> kubectl create -f "8.2.2 pvc-mysql.yaml"
persistentvolumeclaim/mysql-volumeclaim created
# 2. 创建 mysql
> kubectl create -f "8.2.3 mysql.yaml"
deployment.apps/mysql created
# 3. 清理演示环境
> kubectl delete deployment mysql
deployment.apps "mysql" deleted
> kubectl delete pvc mysql-volumeclaim
persistentvolumeclaim "mysql-volumeclaim" deleted
```

### Secret

#### overview

- 可以通过 volume 或 环境变量的形式访问 Secret
- Secret 存储在 tmpfs volumes，这种volumes实际上是在内存中维护了一些文件
- 每个Secret最大限制 1MB
- API Server 会把 Secret 存储在 etcd

#### 命令行创建 Secret 语法

```bash
# 1. 查看帮助
> kubectl create secret --help
Create a secret using specified subcommand.

Available Commands:
  docker-registry 创建一个给 Docker registry 使用的 secret
  generic         从本地 file, directory 或者 literal value 创建一个 secret
  tls             创建一个 TLS secret

Usage:
  kubectl create secret [flags] [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).

# 2. 查看 generic 的帮助
> kubectl create secret generic --help
Create a secret based on a file, directory, or specified literal value.

 A single secret may package one or more key/value pairs.

 When creating a secret based on a file, the key will default to the basename of the file, and the value will default to
the file content. If the basename is an invalid key or you wish to chose your own, you may specify an alternate key.

 When creating a secret based on a directory, each file whose basename is a valid key in the directory will be packaged
into the secret. Any directory entries except regular files are ignored (e.g. subdirectories, symlinks, devices, pipes,
etc).

Examples:
  # Create a new secret named my-secret with keys for each file in folder bar
  kubectl create secret generic my-secret --from-file=path/to/bar

  # Create a new secret named my-secret with specified keys instead of names on disk
  kubectl create secret generic my-secret --from-file=ssh-privatekey=path/to/id_rsa
--from-file=ssh-publickey=path/to/id_rsa.pub

  # Create a new secret named my-secret with key1=supersecret and key2=topsecret
  kubectl create secret generic my-secret --from-literal=key1=supersecret --from-literal=key2=topsecret

  # Create a new secret named my-secret using a combination of a file and a literal
  kubectl create secret generic my-secret --from-file=ssh-privatekey=path/to/id_rsa --from-literal=passphrase=topsecret

  # Create a new secret named my-secret from an env file
  kubectl create secret generic my-secret --from-env-file=path/to/bar.env

Options:
      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in
the template. Only applies to golang and jsonpath output formats.
      --append-hash=false: Append a hash of the secret to its name.
      --dry-run='none': Must be "none", "server", or "client". If client strategy, only print the object that would be
sent, without sending it. If server strategy, submit server-side request without persisting the resource.
      --field-manager='kubectl-create': Name of the manager used to track field ownership.
      --from-env-file='': Specify the path to a file to read lines of key=val pairs to create a secret (i.e. a Docker
.env file).
      --from-file=[]: Key files can be specified using their file path, in which case a default name will be given to
them, or optionally with a name and file path, in which case the given name will be used.  Specifying a directory will
iterate each named file in the directory that is a valid secret key.
      --from-literal=[]: Specify a key and literal value to insert in secret (i.e. mykey=somevalue)
  -o, --output='': Output format. One of:
json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file.
      --save-config=false: If true, the configuration of current object will be saved in its annotation. Otherwise, the
annotation will be unchanged. This flag is useful when you want to perform kubectl apply on this object in the future.
      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The
template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
      --type='': 创建 secret 类型资源
      --validate=true: If true, use a schema to validate the input before sending it

Usage:
  kubectl create secret generic NAME [--type=string] [--from-file=[key=]source] [--from-literal=key1=value1]
[--dry-run=server|client|none] [options]

Use "kubectl options" for a list of global command-line options (applies to all commands).
```

#### 演示：使用 secret

8.3.1 create-secret.yaml

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  root-password: d2FuZ2xpYmluZwo=
  no-root-password: d2FuZ2xpYmluZwo=
# echo "wanglibing" | base64 = d2FuZ2xpYmluZwo=
```

8.3.2 use-secret-from-volume.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-busybox
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    volumeMounts:
      - name: password
        mountPath: "/tmp/apikey"
        readOnly: true
  volumes:
  - name: password
    secret:
      secretName: my-secret
```

8.3.3 use-secret-from-env.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - image: mysql:5.6
          name: mysql
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: my-secret
                  key: root-password
          ports:
            - containerPort: 3306
              name: mysql
```

示例：

```bash
# 1. 准备环境（创建secret）
> kubectl create -f "8.3.1 create-secret.yaml"
secret/my-secret created

# 2. 演示：通过 volume 方式使用 secret
## 2.1 创建 pod
kubectl create -f "8.3.2 use-secret-from-volume.yaml"
pod/secret-busybox created
## 2.2 检查 pod 状态是否 Ready
> kubectl get pod
NAME             READY   STATUS    RESTARTS   AGE
secret-busybox   1/1     Running   0          25s
## 2.3 进入 pod 容器
> kubectl exec -it secret-busybox -- sh
/ # cd /tmp/apikey
/tmp/apikey # ls
no-root-password  root-password
/tmp/apikey # more root-password
wanglibing
/tmp/apikey # more no-root-password
wanglibing
/tmp/apikey # exit

# 3. 演示：通过 环境变量 方式使用 secret
## 3.1 创建 pod mysql
> kubectl create -f "8.3.3 use-secret-from-env.yaml"
deployment.apps/mysql created
## 3.2 检查 pod 状态是否 Ready
> kubectl get pod
NAME                     READY   STATUS    RESTARTS   AGE
mysql-6787d4d46c-bt48p   1/1     Running   1          104s
secret-busybox           1/1     Running   0          5m32s
## 3.3 进入 pod mysql 容器
> kubectl exec -it mysql-6787d4d46c-bt48p -- sh
## 3.4 连接 mysql
# mysql -u root -pwanglibing
mysql> exit

# 4. 清理演示环境
> kubectl delete -f "8.3.3 use-secret-from-env.yaml"
deployment.apps "mysql" deleted
> kubectl delete -f "8.3.2 use-secret-from-volume.yaml"
pod "secret-busybox" deleted
> kubectl delete -f "8.3.1 create-secret.yaml"
secret "my-secret" deleted
```

### ConfigMap

#### configmap 语法

```bash
> kubectl create configmap -h
Create a configmap based on a file, directory, or specified literal value.

 A single configmap may package one or more key/value pairs.

 When creating a configmap based on a file, the key will default to the basename of the file, and the value will default
to the file content.  If the basename is an invalid key, you may specify an alternate key.

 When creating a configmap based on a directory, each file whose basename is a valid key in the directory will be
packaged into the configmap.  Any directory entries except regular files are ignored (e.g. subdirectories, symlinks,
devices, pipes, etc).

Aliases:
configmap, cm

Examples:
  # Create a new configmap named my-config based on folder bar
  kubectl create configmap my-config --from-file=path/to/bar

  # Create a new configmap named my-config with specified keys instead of file basenames on disk
  kubectl create configmap my-config --from-file=key1=/path/to/bar/file1.txt --from-file=key2=/path/to/bar/file2.txt

  # Create a new configmap named my-config with key1=config1 and key2=config2
  kubectl create configmap my-config --from-literal=key1=config1 --from-literal=key2=config2

  # Create a new configmap named my-config from the key=value pairs in the file
  kubectl create configmap my-config --from-file=path/to/bar

  # Create a new configmap named my-config from an env file
  kubectl create configmap my-config --from-env-file=path/to/bar.env

Options:
      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in
the template. Only applies to golang and jsonpath output formats.
      --append-hash=false: Append a hash of the configmap to its name.
      --dry-run='none': Must be "none", "server", or "client". If client strategy, only print the object that would be
sent, without sending it. If server strategy, submit server-side request without persisting the resource.
      --field-manager='kubectl-create': Name of the manager used to track field ownership.
      --from-env-file='': Specify the path to a file to read lines of key=val pairs to create a configmap (i.e. a Docker
.env file).
      --from-file=[]: Key file can be specified using its file path, in which case file basename will be used as
configmap key, or optionally with a key and file path, in which case the given key will be used.  Specifying a directory
will iterate each named file in the directory whose basename is a valid configmap key.
      --from-literal=[]: Specify a key and literal value to insert in configmap (i.e. mykey=somevalue)
  -o, --output='': Output format. One of:
json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file.
      --save-config=false: If true, the configuration of current object will be saved in its annotation. Otherwise, the
annotation will be unchanged. This flag is useful when you want to perform kubectl apply on this object in the future.
      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The
template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
      --validate=true: If true, use a schema to validate the input before sending it

Usage:
  kubectl create configmap NAME [--from-file=[key=]source] [--from-literal=key1=value1] [--dry-run=server|client|none]
[options]

Use "kubectl options" for a list of global command-line options (applies to all commands).
```

#### 演示：创建 configmap

```bash
# 1. 通过 键值对 方式创建 configmap
> kubectl create configmap configmap-1 --from-literal=host=127.0.0.1 --from-literal=port=3000
configmap/configmap-1 created

# 2. 获取 configmap 列表
> kubectl get configmap
NAME               DATA   AGE
configmap-1        2      60s
kube-root-ca.crt   1      4d13h

# 3. 查看 configmap 的详细信息
> kubectl describe configmap configmap-1
Name:         configmap-1
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
host:
----
127.0.0.1
port:
----
3000
Events:  <none>

# 4. 通过 文件导入的方式创建 configmap
> kubectl create configmap configmap2configmap2 --from-file=8.4.0.bootstrap.yaml
configmap/configmap2 created

# 5. 查看 configmap2 的详细信息
> kubectl describe configmap configmap2
Name:         configmap2
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
8.4.0.bootstrap.yaml:
----
server:
  port: 9002
spring:
  application:
    name: report-sso
    logging:
      level:
        root: INFO
        org.springframework.web: INFO
        org.springframework.security: INFO
        org.springframework.security.oauth2: INFO
  cloud:
    nacos:
      # 分布式配置
      config:
        # Data ID
        prefix: com.wanglibing.report-sso.yaml
        # 配置格式
        file-extension: yaml
        # Nacos Server
        server-addr: 172.16.18.206:8848
        refresh:
          # 是否开启动态刷新
          enable: false
      # 服务发现
      discovery:
        # Nacos Server
        server-addr: 172.16.18.206:8848
        enabled: false
    kubernetes:
      config:
        name: name-config
        namespace: default
      reload:
        enabled: true
        mode: polling
        period: 5000
        strategy: shutdown
        monitoring-secrets: true
# 自定义属性，用于测试不同环境的值变化
com:
  wanglibing:
    name: "kevin-prod"
    address: "北京-prod"



Events:  <none>

# 6. 删除演示环境
> kubectl delete configmap configmap2
configmap "configmap2" deleted
> kubectl delete configmap configmap-1
configmap "configmap-1" deleted
```

#### 演示：使用 configmap

8.4.1 configmap-from-literal.yaml

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: config-1
  namespace: default
data:
  host: 127.0.0.1
  port: "3000"
```

8.4.2 configmap-pod-volume.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-2
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    volumeMounts:
      - name: config-volume
        mountPath: /etc/config
  volumes:
      - name: config-volume
        configMap:
          name: config-1
```

8.4.3 configmao-pod-env.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-1
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo hello; sleep 10;done"]
    env:
      - name: HOST
        valueFrom:
          configMapKeyRef:
            name: config-1
            key: host
      - name: PORT
        valueFrom:
          configMapKeyRef:
            name: config-1
            key: port
```

示例：

```bash
# 1. 创建 configmap config-1
> kubectl create -f "8.4.1 configmap-from-literal.yaml"
configmap/config-1 created
# 2. 查看 config-1 的详细信息
> kubectl describe configmap config-1
Name:         config-1
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
host:
----
127.0.0.1
port:
----
3000
Events:  <none>
# 3. 创建 pod（使用 volume 的方式使用 configmap）
> kubectl create -f "8.4.2 configmap-pod-volume.yaml"
pod/busybox-2 created

# 4. 查看 pod 的状态是否 Ready
> kubectl get pod
NAME        READY   STATUS    RESTARTS   AGE
busybox-2   1/1     Running   0          27s

# 5. 进入 pod 内部查看 configmap
> kubectl exec -it busybox-2 -- sh
/ # cd /etc/config/
/etc/config # ls
host  port
/etc/config # more host
127.0.0.1/etc/config # more port
3000/etc/config # exit

# 6. 创建 pod（使用环境变量的方式使用 configmap） busybox-1
> kubectl create -f "8.4.3 configmao-pod-env.yaml"
pod/busybox-1 created

# 7. 检查 busybox-1 的状态是否 Ready
> kubectl get pod
NAME        READY   STATUS    RESTARTS   AGE
busybox-1   1/1     Running   0          2m8s
busybox-2   1/1     Running   0          11m

# 8. 进入 pod busybox-1 读取 configmap
> kubectl exec -it busybox-1 -- sh
/ # echo $HOST
127.0.0.1
/ # echo $PORT
3000
/ # exit

# 9. 清理演示环境
> kubectl delete pod busybox-1
pod "busybox-1" deleted
> kubectl delete pod busybox-2
pod "busybox-2" deleted
> kubectl delete configmap config-1
configmap "config-1" deleted
```

## Debug

### pod 一直是 ContainerCreating 状态

```bash
# 1. pod 一直是 ContainerCreating 状态
> kubectl get pod -o wide -w
NAME      READY   STATUS              RESTARTS   AGE   IP       NODE            NOMINATED NODE   READINESS GATES
test-pd   0/2     ContainerCreating   0          7m    <none>   192.168.0.101   <none>           <none>
# 2. 使用 kubectl describe 排查问题
> kubectl describe pod test-pd                                                                                                          ─╯

Name:         test-pd
Namespace:    default
Priority:     0
Node:         192.168.0.101/192.168.0.101
Start Time:   Mon, 19 Jul 2021 20:41:51 +0800
Labels:       <none>
Annotations:  <none>
Status:       Pending
IP:
IPs:          <none>
Containers:
  busybox1:
    Container ID:
    Image:         busybox
    Image ID:
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/sh
    Args:
      -c
      while true; do echo hello; sleep 10;done
    State:          Waiting
      Reason:       ContainerCreating
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /test-pd from test-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-dxh92 (ro)
  busybox2:
    Container ID:
    Image:         busybox
    Image ID:
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/sh
    Args:
      -c
      while true; do echo hello; sleep 10;done
    State:          Waiting
      Reason:       ContainerCreating
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /test-pd from test-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-dxh92 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             False
  ContainersReady   False
  PodScheduled      True
Volumes:
  test-volume:
    Type:          HostPath (bare host directory volume)
    Path:          /data
    HostPathType:  Directory
  default-token-dxh92:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-dxh92
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                 node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason       Age                    From               Message
  ----     ------       ----                   ----               -------
  Normal   Scheduled    10m                    default-scheduler  Successfully assigned default/test-pd to 192.168.0.101
  Warning  FailedMount  3m27s (x3 over 7m57s)  kubelet            Unable to attach or mount volumes: unmounted volumes=[test-volume], unattached volumes=[test-volume default-token-dxh92]: timed out waiting for the condition
  Warning  FailedMount  106s (x12 over 10m)    kubelet            MountVolume.SetUp failed for volume "test-volume" : hostPath type check failed: /data is not a directory
  Warning  FailedMount  72s                    kubelet            Unable to attach or mount volumes: unmounted volumes=[test-volume], unattached volumes=[default-token-dxh92 test-volume]: timed out waiting for the condition
```

### pvc一直是pending状态

```bash
# 1. pvc一直是pending状态
> kubectl get pvc
NAME        STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
hello-pvc   Pending                                                     73s
# 2. 使用 kubectl describe 排查问题
> kubectl describe pvc hello-pvc                                                                                 ─╯
Name:          hello-pvc
Namespace:     default
StorageClass:
Status:        Pending
Volume:
Labels:        <none>
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       <none>
Events:
  Type    Reason         Age                  From                         Message
  ----    ------         ----                 ----                         -------
  Normal  FailedBinding  2s (x13 over 2m53s)  persistentvolume-controller  no persistent volumes available for this claim and no storage class is set
```