```
서버에서 처리해야 하는 업무
1. 서버 TCP/IP 대기, 소켓 연결
2. Http 요청 메시지 파싱해서 읽기
3. Http 메서드 확인, 어떤 요청인지 확인
4. Content-Type 확인
5. Http 메시지 바디 내용 파싱
6. 저장 프로세스 실행

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

7. 비즈니스 로직 실행
ex) 데이터베이스에 저장 요청

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

8. Http 응답 메시지 생성 시작
9. TCP/IP에 응답 전달, 소켓 종료

서블릿을 활용하면 7번을 제외한 모든 일이 자동적으로 이루어진다.

```

### Servlet
특징
```
@WebServlet(name = "helloServlet", urlPatterns = "/hello")
// urlPatterns에 붙은 경로에서 요청이 오면 이 클래스가 실행이 됨
public class HelloServlet extends HttpServlet{
	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response){
		//애플리케이션 로직
		//HTTP 요청 정보를 편리하게 사용할 수 있는 HttpServletRequest
		//HTTP 응답 정보를 편리하게 제공할 수 있는 HttpServletResponse
		//개발자는 Http 스펙을 매우 편리하게 사용
	}

}
```

### Http 요청, 응답 흐름
- Http 요청시
1) WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출
2) 개발자는 Request 객체에서 Http 요청 정보를 꺼내서 사용
3) 개발자는 Response 객체에 Http 응답 정보를 입력
4) WAS는 Response 객체에 담겨있는 내용을 바탕으로 Http 응답 정보를 생성

### 서블릿 컨테이너
1) 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함
2) 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출,  종료하는 생명주기 관리
3) 서블릿 객체는 싱글톤으로 관리
>> 고객의 요청이 올 때마다 계속 객체를 생성하는 것은 비효율<br/>
>> 최초 로딩 시점에 서블릿 객체를 미리 만들어두고 재활용<br/>
>> 공유 변수 사용 주의<br/>
4) JSP도 서블릿으로 변환되어서 사용
5) 동시 요청을 위한 멀티 쓰레드 처리 지원
