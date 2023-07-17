# 基于 axios 请求库封装

```ts
/**
 *
 * ================================================================================
 * ===================================测试代码=====================================
 * ================================================================================
 *
 */
import Request from '.'

const instance = new Request('https://xiyuer.club/api/v1', 10000, {
    // 实例拦截器
    requestInterceptor: {
        onFulfilled(config) {
            console.log('实例请求成功拦截')
            return config
        },
        onRejected(error) {
            console.log('实例请求失败拦截')
            return error
        },
    },
    responseInterceptor: {
        onFulfilled(value) {
            console.log('实例响应成功拦截')
            return value.data
        },
        onRejected(error) {
            console.log('实例响应失败拦截')
            return error
        },
    },
})

type IData = any[]

const getBanner = () => {
    instance
        .get<IResponse<IData>>({
            url: '/banner',
            // 接口拦截器
            requestInterceptor: {
                onFulfilled(config) {
                    console.log('接口请求成功拦截')
                    return config
                },
                onRejected(err) {
                    console.log('接口请求失败拦截')
                    return err
                },
            },
            responseInterceptor: {
                onFulfilled(data) {
                    console.log('接口响应成功拦截')
                    return data
                },
                onRejected(err) {
                    console.log('接口响应失败拦截')
                    return err
                },
            },
        })
        .then((res) => {
            console.log(res)
        })
}
getBanner()
```
