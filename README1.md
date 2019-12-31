# book app

## table:books

| book_id | book_name |
|:-------:|:---------:|
|   101   |     c     |
|   102   |    java   |

## table:book_stock

| stock_id | book_id | quantity |
|----------|---------|----------|
| 1        | 101     | 100      |
| 2        | 102     | 50       |


## table:orders

| order_id | username | book_id | quantity | status    |
|----------|----------|---------|----------|-----------|
| 1        | a        | 101     | 5        | ordered   |
| 2        | b        | 101     | 3        | delivered |
| 3        | c        | 102     | 2        | ordered   |
| 4        | d        | 101     | 1        | canceled  |
