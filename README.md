<h1>React-Query</h1>
<div>
  <div>
    <span>데이터 Fetching , 캐싱 , 동기화 , 서버의 데이터 업데이트 , 에러 핸들링 등 비동기 과정을 더욱 편하게 하는데 사용되는 React의 라이브러리</span>
  </div>
  <div>
    <h2>How to adjust ReactQuery in my project?</h2>
    <div>
            1) Make a React Project with CRA or Vite    
                CRA : npx create-react-app my-app
                Vite : npm create vite@latest
            2) react-query download
                npm : npm i @tanstack/react-query
                pnpm : pnpm add @tanstack/react-query
                yarn : yarn add @tanstack/react-query
            2-1) Use CDN in HTML files 
                 : <script src="https://unpkg.com/@tanstack/react-query@4/build/umd/index.production.js"></script>
            3) Start React Query in your React project
                 ```
                 ex) <App.js> 
                  import React from 'react'
                  import ReactDOM from 'react-dom/client'
                  import App from './App'
                  import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
                  import { ReactQueryDevtools } from '@tanstack/react-query-devtools'
                  import './index.css'
                  
                  const queryClient = new QueryClient();

                  ReactDOM.createRoot(document.getElementById('root')).render(
                    <QueryClientProvider client={queryClient}>
                      <App />
                      <ReactQueryDevtools initialIsOpen={false} />
                    </QueryClientProvider>
                  )
                  ```
    </div>
  </div>  
</div>
  
<div>
  <h2>How to use React-Query?</h2>
  <div>
    <h3>useQuery</h3>
    <p>
      useQuery() 는 기본적인 R.Q(React-Query 이하 R.Q로 통칭)의 데이터를 불러오는 함수이다.
      useQuery() 는 인수로 queryKey, queryFunc(callback 함수)를 받는다.
      
      queryKey = R.Q가 불러온 데이터를 따로 키로 지정해둬서 cached 해놓는다. queryKey 는 string 타입으로 작성해도 되지만 배열형식으로 작성해서 해당 데이터 값의 키를 더 정확하게 지정 해 줄 수 있다.
      queryFunc = R.Q가 데이터를 불러오기 위해 실행할 함수.
      <pre>
        <code>
          ex)<MyApp.jsx>
          import { getData } from '../../api/dataapi'
          import './App.css'
          import axios from 'axios';

          const MyApp = () => {
              const [number, setNumber] = useState(1);
              const queryFn = (number) => {
                return axios.get(`https://jsonplaceholder.typicode.com/posts/${number}`).then(res => res.data);
              }

              const { isLoading, data : user, refetch } = useQuery({queryKey : ['getData',{type: 'firstData'}] , queryFn : getData});
              const userId = user?.userId
              
              const { status , fetchStatus , data : user2 , isError : isError2  } = useQuery({queryKey : ['getData',{type: 'secondData'}] , queryFn : () => queryFn(number) , enabled : !!userId});

              const refetchFunc = () => {
                console.log(`리패치를 해보자`)
                refetch();
              }

              return(
                <>
                  <div className="App">
                    {userId}는 유저의 아이디이다.
                  </div>
                  <div>
                    {isLoading && <div>Loading...</div>}
                  </div>
                  <button onClick={refetchFunc}></button>
                </>
              )
          }

          export default MyApp;
        </code>
      </pre>
    <p>
  </div>
  <div>
    <h3>useQueries</h3>
  </div>
  <div>
    <h3>useInfiniteQuery</h3>
  </div>
</div>
