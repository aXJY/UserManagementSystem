//获取所有用户信息
http://localhost:3000/

//获取id为1的用户信息
http://localhost:3000/users/1

//获取公司的所有信息
http://localhost:3000/companies

//获取单个公司的信息
http://localhost:3000/companies/1

//获取所有公司id为3的用户
http://localhost:3000/companies/3/users

//根据公司名字获取信息
http://localhost:3000/companies?name=Microsoft

//根据多个名字获取公司信息
http://localhost:3000/companies?name=Microsoft&name=Apple

//获取一页中只有两条数据
http://localhost:3000/companies?_page=1&_limit=2

//升序排序 asc升序 desc降序
http://localhost:3000/companies?_sort=name&order=asc

//获取年龄21及以上的
http://localhost:3000/users?age_gte=21

//获取年龄在20-25之间的
http://localhost:3000/users?age_gte=20&age_lte=25

//搜索用户信息
http://localhost:3000/users?q=洁