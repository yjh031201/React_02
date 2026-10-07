# 202230220 양종호
# 2026-10-07
### await이 없어도 async를 붙여 두는 이유
1. 일관성 유지
   >같은 프로젝트에서 어떤 페이지는 async, 어떤 페이지는 일반 function이면 혼란스러울 수 있음   
2. 확장성   
   >지금은 더미데이터를 사용했지만 나중에 DB나 API에서 데이터를 가져오면 await fetch(...) 같은 코드가 들어갈 수 있기 때문에, 미리 붙여두면 수정할 필요가 없다   
3. React Server Component 호환성   
   >Server Component는 Promise를 반환할 수 있어야 하고,   
   >Next.js는 내부적으로 async 함수 패턴에 맞춰 최적화된 렌더링 파이프라인을 갖고 있어서   
   >async가 붙어 있어도 불필요한 오버헤드가 거의 없다.   
# 2026-09-30
### 서버 렌더링
1. 서버 렌더링에는 발생 시점에 따라 두 가지 유형이 있음.
   >정적 렌더링   
   >>빌드 시점이나 재검증 중에 발생, 결과는 캐시됨
   
   >동적 렌더링   
   >>클라이언트 요청에 대한 응답으로 요청 시점에 발생
2. Prefetching(프리페칭: 미리 가져오기)
   >사용자가 해당 경로로 이동하기 전에 백그라운드에서 해당 경로를 로드해서   
   >사용자가 클릭하기전에 렌더링하여 사용자가 느끼기에 굉장히 빠르게 느껴짐

# 2026-09-23
### Link Component
1. ``` <Link> ```를 통해서 페이지간 이동이 가능
   >예시   
   >```   
   ><Link href={"/"}>Home</Link> | <Link href={"/blog"}>Blog</Link>   
   >```
2. searchParam
   >URL의 쿼리 문자열을 읽는 방법   
   >예시) /product?category=shoes&page=2   
   >여기서 ?뒤에 오는 category=shoes&page=2가 search param이다.   
   >예제   
   >```
   >export default async function ProductPage({
   > searchParams
   >}:{
   >    searchParams: Promise<{ id?: string; name?: string}>
   >}) {
   >    const {id ="non id", name="non name"}= await searchParams
   >    return(
   >     <div>
   >         <h1>Product Page</h1>
   >         <p>id: {id}</p>
   >         <p>name: {name}</p>
   >     </div>
   > )
   >}
   >```
# 2026-09-16
### Folder and file conventions
1. 라우팅 그룹 및 비공개 폴더
   >라우트 그룹을 사용하여 URL을 변경하지 않고 코드를 정리할 수 있다.   
   >라우팅되지 않는 파일들은 _folder라는 비공개 다렉토리에 함께 저장한다.      
2. 병렬과 가로채기 라우팅
   >슬롯 기반 레이아웃이나 모달 라우팅과 같은 특정 UI패턴에 적합   
   >인터셉트 패턴을 사용해 URL을 변경하지 않고도 현재 레이아웃 내에서 다른 경로를 렌더링 할 수 있다   
   >예시) 메인 페이지 + 사이드바   
# 2026-09-02
### pnpm vs npm
1. pnpm   
   >하드 링크 기반의 효율적인 저장 공간 사용
   >>패키지를 한 번만 설치하여 글로벌 저장소에 저장하고,   
   >>각 프로젝트의 node modules 디렉토리에는 설치된 패키지에 대한 하드링크가 생성됨

   >빠른 패키지 설치 속도
   >>이미 설치된 패키지는 재사용함 다시 다운로드 x

   >효율적인 종속성 관리   
   >다른 패키지 매니저의 비효율성을 개선한 패키지 관리자이다.   
   
* 우리가 파일 이라고 부르는 것은 세 부분으로 나눠져 있음   
   1. Directory Entry : 파일 이름과 해당 inode 번호를 매핑 정보가 있는 특수한 파일.   
   2. inode : 파일 또는 디렉토리에 대한 모든 메타데이터를 저장하는 구조체.   
   3. data blocks : 실제 데이터가 존재하는 영역   
* 하드링크를 생성하면 디렉토리 엔트리에 매핑 정보가 추가 되어 동일한 inode를 가르키게 됨   
* 따라서 원본과 하드링크는 완전히 동일한 파일   
* 원본과 사본의 개념이 아님   
