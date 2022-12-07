Первым делом заходим на биржу Bittrex, открываем BTC/USD ![image](https://user-images.githubusercontent.com/53054649/206195646-19386693-2d82-43e8-8731-1da61f112778.png)

Нажимаем F12, переходим во вкладку Network, видим что к нам приходяд разные элементы данных. ![image](https://user-images.githubusercontent.com/53054649/206196073-19ef90c1-12b4-49d8-87a1-1fd5cde455da.png)

Опускаемся вниз списка и видим первый нужный нам элемент данных с названием recent. ![image](https://user-images.githubusercontent.com/53054649/206196375-07edefc2-5d3d-494e-aa06-bb8232596884.png)

Отправляет сообщение в начале каждой свечи (на основе подписанного интервала) и когда на рынке произошли сделки.
Следует обратить внимание, что это означает, что на активном рынке мы будем получать множество обновлений в течение каждого интервала свечей по мере 
совершения сделок. Мы всегда будете получать обновление в начале каждого интервала. Если еще не произошло ни одной сделки, это обновление будет
заполнителем с 0 объемами, который переносит закрытие предыдущего интервала в качестве значений OHLC текущего интервала.

Данный запрос предоставляет данные по свечам между BTC\USD за последний час.
Эти данные используются для построения отображения свечей (`I`)

```bash
curl https://api.bittrex.com/v3/markets/BTC-USD/candles/trade/HOUR_1/recent
```

Example of output data with comments:
```json5
{
[
  {
    // Время начала свечи
    "startsAt": "string (date-time)", 
    // Цена первой сделки внутри интервала
    "open": "number (double)", 
    // Цена самой высокой сделки внутри интервала
    "high": "number (double)", 
    // Цена наименьшей сделки внутри интервала
    "low": "number (double)", 
    // Цена последней сделки внутри интервала
    "close": "number (double)", 
    // Фактический обьем сделок на интервале
    "volume": "number (double)", 
    // Обьем сделок на интервале
    "quoteVolume": "number (double)" 
  }
]
```

Пример выполнения запроса в терминале
![image](https://user-images.githubusercontent.com/53054649/206197255-43b22d53-cae1-4950-954d-a6e203e80d30.png)


Ниже можно увидеть элемент данных с названием "trades"
![image](https://user-images.githubusercontent.com/53054649/206197622-84287fa1-cb5c-4460-975e-3977b264392c.png)

На его основе строится Лента сделок (Trade History). 


Данный запрос предоставляет данные по прошедшим сделкам.

```bash
curl https://api.bittrex.com/v3/markets/BTC-USD/trades
```
Example of output data with comments:
```json5
{
[
  {
   "sequence": "int",
  "marketSymbol": "string",
  "deltas": [
    {
      // Уникальный номер сделки
      "id": "string (uuid)", 
      // Дата совершения сделки
      "executedAt": "string (date-time)", 
      // Обьем совершенной сделки
      "quantity": "number (double)", 
      // Курс сделки
      "rate": "number (double)",
      // Покупка или продажа
      "takerSide": "string" 
  }
]
```
![image](https://user-images.githubusercontent.com/53054649/206198999-3af1e6c8-0e6b-4635-854e-ad586ff14017.png)


Еще ниже в панели инструментов находим элемент данных с названием "orderbook?depth=500"
![image](https://user-images.githubusercontent.com/53054649/206199280-1a60e825-2824-4d46-818d-4aa2159e1d91.png)


Данный запрос предоставляет данные по Order Book.

```bash
curl https://api.bittrex.com/v3/markets/BTC-USD/orderbook?depth=500 
```
Example of output data with comments:
```json5
{
[
  {
   "marketSymbol": "string",
   "depth": "int",
   "sequence": "int",
   // Заявки на покупку
   "bidDeltas": [ 
    {
      // Количество ( в нашем случае BTC)
      "quantity": "number (double)", 
      // Курс
      "rate": "number (double)"
    }
  ],
  //  Заявки на продажу
  "askDeltas": [
    {
      // Количество ( в нашем случае BTC)
      "quantity": "number (double)",
      // Курс
      "rate": "number (double)"
  }
]
```
