
# 테스트 환경 설정

#### 테스트 환경 (서버 주소)을 변경하는 방법을 소개합니다.

Nugu 서비스를 사용하기 전 (initialize 단계가 적당합니다.) NuguServerInfo.resourceServerAddress 값을 변경합니다.
아래 심사용과 테스트용 주소가 준비되어 있습니다.

   * 심사용 : `review-dghttp.sktnugu.com` 
   * 테스트용 : `test-dghttp.sktnugu.com`

   ```swift
   
    // NuguCenralManager.swift 
    
    private init() { 
        NuguServerInfo.resourceServerAddress = "https://review-dghttp.sktnugu.com"
    }
   ```


