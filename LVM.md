### LVM(Logical Volume Manager)이란?
물리적인 하드디스크 여러개를 논리적인 디스크로 할당하여 관리할 수 있게 해주는 프로그램.  
기존에 사용중인 디스크의 공간을 확장하는데 있어 유용하며 안정성이 높다.  
즉, a라는 파티션에 용량이 100G인데 용량이 부족하여 확장해야한다면 디스크만 추가하여 설정만 해준다면 간단히 용량이 추가된다.  
또한 불필요하게 많은 용량을 가지고 있는 파티션에서도 용량을 줄여 다른 파티션에 용량을 활용 가능하다.  

#### LVM 관련 용어
- Partition - 디스크의 사용 구역을 나누는 것
- PV(Physical Volume) - LVM으로 사용위해 형식을 변환 시킨 것(물리적 공간)
- PE(Physical Extent) - 물리적 저장공간의 최소 단위(기본 4MB)
- LV(Logical Volume) - 사용자가 다루는 실질적인 공간(논리적 공간)
- LE(Logical Extent) - 논리적 저장공간의 최소 단위(기본 4MB)
- VGDA(Volume Group Descriptor Area) - PV,PE,LV,LE 할당 상태 등 LVM의 전체 구조를 저장
