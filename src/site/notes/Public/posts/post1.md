---
{"dg-publish":true,"permalink":"/public/posts/post1/","title":"Open Project docker 16-slim version: admin/admin отсутствует [[post1|Read]]","tags":["blog","DevOps"]}
---


<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



# Open Project docker 16-slim version: admin/admin отсутствует

После разворачивания Open Project согласно офф гайду мы должны зайти в админ учётку по кредам admin/admin однако не срабатывает и пишет что либо что то некорректно ввёл либо юзера нет. Оказывается его реально нет! Точнее как: там может оказаться пользователь без логина. Вообщем лезть создавать админа надо самому

1. Создаём юзера (можно и в GUI)
2. Cуём ручки в контейнер 
```shell
docker exec -it openproject-db-1 psql -U postgres -d openproject
```    
3.  Делаем нашу болванку из пункта 1 админом
	1.  Шиза moment: пользователь жеж создался?
	```sql
	SELECT id, login, admin, status FROM users WHERE login = '<логин юзера из пункта 1>';
	```
	2. Даём этому юзеру клеймо админа
	```sql
    UPDATE users SET admin = true WHERE login = '<логин юзера из пункта 1>';
    ```
	3. Так как админ вышел из чата учётку сами активируем
    ```sql
    UPDATE users SET status = 1 WHERE login = '<логин юзера из пункта 1>';
    ```



</div></div>


[[Public/Index\|Главная страница]]