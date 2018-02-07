# RubleCoin
Token for sponsorship of the russian president election campaign

h2 Использование смарт-контракта RubleCoin
h3 (на примере работы через Mist)

1.	Для работы и приема средств в основном блокчейне контракт нужно выгрузить в основой Ethereum-блокчейн

2.	В контракте определены несколько вспомогательных классов-контрактов. Вам нужно запустить Ruble Coin Crowdsale   

3.	В качестве параметра нужно передать значение rate (курс). 
В связи с тем, что смарт-контракты не поддерживают работы с дробными числами rate должно быть целым числом от 1 до 999. Как его рассчитать? Если мы хотим, чтобы без учета скидок 2500 RUBC стоили 400 рублей, то нужно рассчитать, сколько это будет в эфирах. Если курс доллара составляет 56 рублей, курс эфира составляет 1100 долларов, то 400 рублей это примерно 400/(56 * 1100) = 0,00649… Rate это количество десятитысячных долей эфира, которые нужно заплатить за 2500 RUBC. В нашем случае это будет примерно 65. 

Курс эфира и доллара может меняться в процессе кампании по продаже токенов, поэтому в контракте предусмотрена функция изменения rate. 


4.	После загрузки контракта в сеть у него появится адрес типа такого https://gyazo.com/6d2460cbb904234286e601cb73fd9016
Именно на этот адрес инвесторам предстоит отправлять вам эфир. 

5.	После отправки контракта в сеть в его параметрах появится адрес токена RUBC https://gyazo.com/939afb017d075d51334baa7efc3b28ec
Все кто хочет, чтобы информация об этом токене (например, баланс на счету) отображался в Mist должны, добавить этот адрес в разделе 

Contracts -> Custom Tokens -> Watch Token https://gyazo.com/df2c40e5f5fba2e17cfca9881194f1d0
 Интерфейс добавления будет выглядеть так: https://gyazo.com/30898b3bf45703018d29200172b6ecd1

6.	 В интерфейсе контракта будут доступны его текущие параметры

•	Name – название контракта (будет видно покупателю токена)
•	Rate - курс для расчета стоимости токена
•	IsRunning – переменная отражающая не завершена ли продажа токенов
•	EndTime – время завершения продажи токенов
•	Discount End Time – время завершения продажи токенов со скидкой
•	Wei raised – сколько всего эфиров было переведено на адрес контракта. Высчитывается в wei. Wei это частица эфира. В одном эфире содержится десять в восемнадцатой степени wei. 
•	IsDiscount – действует ли сейчас скидка при продаже токенов
•	TokensMinted – сколько всего токенов было выпущено с учетом дробных долей. Т.е. если выпущено всего два токена, то в этом разделе будет отображаться значение 200. 
•	StartTime – время загрузки контракта в сеть и начала продажи токенов
•	MinimumSupply – минимальное количество токенов, которые могут быть проданы за одну транзакцию
•	Owner – адрес владельца контракта. На этот адрес будет переведено 0,11% от выпущенных токенов и 1% от собранных средств
•	FundAddress2 – адрес, на который будет переведен 1% от собранных средств. 
•	ContractStatus – описание, в каком состоянии сейчас контракт (например, Sale with discount)
•	FundAddress – адрес, на который будет переведено 98% собранных средств
•	Token – адрес-идентификатор токена

7.	Также там можно будет вызвать ряд функций https://gyazo.com/43f54ae17162100054b169119ad98b32

•	SetRate - Установить rate
•	Full Price Stage – перевести контракт в стадию, когда токены продаются без скидки
•	Finish Crowdsale – завершить продажу токенов
•	TransferOwnership - изначально Владельцем контракта становится тот, кто загрузил контракт в сеть. Только с этого же кошелька возможен вызов функций SetRate, FullPriceStage,  FinishCrowdSale, TransferOwnership. Но Владелец может передать свои права на другой адрес при помощи функции TransferOwnership. 

8.	Под интерфейсом контракта можно отслеживать события генерируемые контрактом. Для этого нужно поставить галочку в поле Watch contract events https://gyazo.com/42f231d9aa5376d14fdab12a079c9fa6
В событиях будет выводиться кто и когда совершил перевод на адрес контракта, сумма эфира (в wei), сколько он получил токенов (для получения целого значения токенов это значение нужно поделить на сто) и сколько всего токенов было выпущено к этому моменту. 
Также добавлены вспомогательные поля integer_value (это значение сколько было переведено десятитысячных долей эфира округленное до целого числа вниз). А также поле integer_amount – округленная до целого числа вниз сумма выпущенных токенов). 


9.	Все поступающие на счет контракта средства автоматически переправляются на кошелек Владельца контракта (1%), на счет фонда (98%) и еще на один кошелек указанный при загрузке контракта в сеть (1%).

10.	0,11% от купленных токенов отправляется на кошелек Владельца контракта

