# Promo video for galtproject.io 

## First screen video

### Text and voice
|№|English text|Russian text|Screen Action|
|------|-------|----------|-------|
|1|Galt Project is first decentralised non-government land and real estate registry and a self-governance platform based on Ethereum blockchain|Galt Project - это первый децентрализованный негосударственный реестр прав собственности на землю и недвижимость, а так же платформа для самоуправления на блокчейне Ethereum |-|
|2|Here anyone can register one's land plots or real estates as tokens, trade them on Ethereum without borders with all legal formalities or create a community of homeowners for voting and property management |Здесь каждый может зарегистрировать свой земельный участок или недвижимость, как токены, торговать ими на блокчейне Ethereum со всеми юридическими формальностями или создать сообщество домовладельцев для голосований и управления общей собственностью |-|
|3|Most of the operations, like land survey, land trading or voting are performed by smart contracts, but also protocol provides governance system to resolve disputes and interact with government agencies |Большинство операций, такие как межевание земли, торговля землей и недвижимостью, голосования выполняются умными контрактами, но так же протокол предоставляет систему самоуправления участников для разрешения споров и взаимодействия с государственными органами |-|
|4| For more information watch further videos, test sotware, read whitepaper and join us on telegram!  | Для того, чтобы узнать больше - смотрите дальнейшие видео, тестируйте платформу, читайте вайтпейпер и присоединяйтесь к нам в телеграм канале! |-|


### Screen Action
- show token list and tokens on the map in Austrian city. Shouls be 2 tokens - land and building (town hall and land under town hall);
- show point cloud representaion;
- show split operation of land plot and new both representations as map view and point cloud;

### Additional requirements
Video sequence and text should be consistent in duration.

## Key Features - Consistent Geospatial Registry

### Text and voice

|№|English text|Russian text|Screen Action|
|------|-------|----------|-------|
|1|In Galt Project land plots and real estate are stored on Ethereum as ERC721 tokens with coresponding geospatial data|В Galt Project земельные участки и недвижимость хранятся в блокчейне Ethereum, как токены стандарта ERC721 с привязанными к ним гео-пространственными координатами |Открыт экран просмотра токенов. На нем показаны три токена в списке слева: токен земельного участка, токен этажа здания и токен квартиры, с заданной заранее площадью.|
|2|There are 3 types of tokens: `land plots tokens`, `building areas tokens`, and `pre-defined real-estate tokens`. You can see them on the left panel and on the map|Существует три типа токенов: `токены земельных участков`, `токены площадей зданий` и `предопределенные токены недвижимости`. Вы можете их видеть слева на панели и на карте. |Открыт экран просмотра токенов, как выше. Мышка движется сначала к панели с токенами, а потом к карте.|
|3|`Land plot tokens` represent particular land plot with unique geographical coordinates. Each token stores information about the boundaries of the land plot in smart contract in the form of coordinates of the vertices of the plot. You can see token contains accurate coordinates in different form: Latitide and Longitude, UTM or Universal Transverse Mercator and Geohash. Coordinates are three-dimensional. Every point of land plot has an Altitude coordinate in metres above sea level. You can see it here.  All this information is stored on Ethereum blockchain. |Токены земельных участков представляют собой конкретные земельные участки с уникальными географическими координатами. Каждый токен хранит информацию о границах земельного участка в умном контракте в виде координат вершин участка. Вы можете видеть, что токен содержит точные координаты в различной форме: Широта и Долгота, UTM или Универсальная поперечная проекция Меркатора и Геохэш. Координаты трехмерные. Каждая точка земельного участка имеет высотную координату в метрах над уровнем моря. Можно посмотреть их здесь. Вся эта информация хранится в блокчейне Ethereum.| Пользователь нажимает на токен в списке. Участок выделяется на карте. Пользователь нажимает на маркер и переключается между различными представлениями координат, включая трехмерные.|
|4|`Building area tokens` are same as Land plot tokens, except that each of them do not represent a land plot, but a specific area of a building. As Land plot tokens, they store geographical coordinates. I will show you. Unlike `Land plot tokens`, `Building area tokens` store Altitude coordinate as a Height above ground in meters. |Токены площадей зданий такие же, как токены земельных участков, кроме того, что каждый из них представляет не земельный участок, а конкретную площадь здания. Как и токены земельных участков, они хранят географические координаты. В отличие от токенов земельных участков, токены площадей зданий хранят координаты высот в виде высоты над землей в метрах.| Пользователь нажимает на токен, он выделяется на карте. Показывает координаты.|
|5| Also there is a three-dimensional view for `Building area tokens`. This view is based on the building information model and stored in IPFS. |Так же есть возможность вывести трехмерное изображение токена, которое основано на информационной модели здания, хранящейся в IPFS.| Переходим из карты в трехмерное изображение токена, показываем, идем обратно.|
|6|Sometimes it's not necessary to store information about precise coordinates for part of the building. For example you probably don't need to store geographic coordinates of your appartment. In that case it's enought to store building address and appartment number or any other identification data. For that purpose you can use `pre-defined real-estate tokens`.|Иногда нет необходимости хранить информацию о точных координатах для части здания. Например, вам, вероятно, не нужно хранить географические координаты вашей квартиры. В этом случае достаточно хранить адрес здания, номер квартиры или любые дополнительные идентификационные данные. Для этого вы можете использовать `предопределенные токены недвижимости`.|Остаемся на экране с токенами.|
|7|For example here I have my appartment token. Token contains geographic coordinates of my apartment house, address and appartment number. The difference is that geographic coordinates are not unique. All appartments in the building have same coordinates. Also appartment area is set manually, it's not calculated by smart contract.|Например, у меня есть токен моей квартиры. Токен содержит географические координаты моего многоквартирного дома, адрес и номер квартиры. Разница в том, что географические координаты не являются уникальными. Все квартиры в здании имеют одинаковые координаты. Также площадь квартиры задана вручную, а не рассчитана умным контрактом.| Нажимаем на токен квартиры, отображаем его на карте, видим, что там много других токенов. Нажимаем на свой маркер, показываем на координаты и на площадь.|
|8|You can use your tokens for trading or other commercial purposes. Or you can create a comminity of homeowners for self-governance. For more information watch further videos, test sotware, read whitepaper and join us on telegram! |Вы можете использовать свои токены для купли-продажи или любых других коммерческих целей. Или вы можете создать сообщество домовладельцев для самоуправления.Для того, чтобы узнать больше - смотрите дальнейшие видео, тестируйте платформу, читайте вайтпейпер и присоединяйтесь к нам в телеграм канале!|Показываем ссылки.|



## Key Features - Smart contract Land surveying

### Text and voice

|№|English text|Russian text|Screen Action|
|------|-------|----------|-------|
|1|In Galt Project you can use smart contracts to split and merge land plots and building areas.|В Galt Project вы можете использовать умные контракты для разделения и обьединения токенов земельных участков и площадей зданий.|Показываем экран с токенами|
|2|In case of split operation special algorithms ensure that borders of the new land plot or building area will correspond to the old one. Let's see how it works.|В случае операции разделения специальные алгоритмы гарантируют, что границы нового земельного участка или площади здания будут соответствовать общий старым границам. Посмотрим, как это работает. |Показываем экран с токенами|
|3|For example I want to split my current land plot with vineyard in two parts and sell one part to my friend Bob.|Для примера я хочу разделить мой текущий участок земли с виноградником на две части и продать одну часть моему другу Бобу.|Показываем экран с токенами. Показываем виноградник в облаке точек и переходим обратно.|
|4|On the left panel, you can see my land plot token. I will choose split operation in menu.|На левой панеле Вы видите токен моего земельного участка. Я выберу операцию разделения из меню.|Выбираем сплит|
|5|I need to set contour of a new land plot. I can point it on a map, or fill the coordinates in form. Ok, let's do that. (pause) Here I can see information about area before and after split.  |Сначала я должен определить контур нового земельного участка. Я могу указать контур на карте или ввести координаты вручную. Давайте это сделаем (пауза).....Здесь вы можете увидеть информацию о площади земельного участка до разделения и после.|Выбираем сплит. Выбираем новый контур, показываем верху значения площади.|
|6|After setting the new contour i need to aprove my land plot token to smart contract by signing transaction. |После задания контура я должен разрешить умному контракту выполнять операции с моим токеном.|Делаем апрув.|
|7|Now we can start split operation. During split operation land plot token is transfered to smart contract. Smart contract performs calculations, changes borders of source land plot and creates new one. |Теперь мы можем начать операцию разделения участка. Во время выполнения этой операции токен земельного участка передается умному контракту. Умный контракт выполняется вычисления, меняет границы исходного земельного участка и создает новый.|Ничего не делаем|
|8|- |-|Нажимаем сплит и отправляем транзакцию.|
|9|To performs split operation we need to perform multiple transactions. For better user experience we will use local built-in temporary wallet. We will transfer ETH to pay for gas. Unspent ETH will be sent back. |При этом нам надо выполнить несколько последовательных транзакций. Для большего удобства мы используем локальный встроенный временный кошелек. Мы отправим Эфир для оплаты газа. То, что не будет потрачено - автоматически вернется обратно.|Показываем временный кошелек и отправляем ETH. Запускаем и показываем очередь транзакций.|
|10|After all transaction were executed we can withdraw land plot tokens and sell one of them to Bob.|После того, как все транзакции были выполнены, мы можем вернуть два токена земельных участка и продать один из них Бобу.|Забираем токены. Показываем на карте, потом в облаке точек.|
|11|But we decided not to do it and merge our two land plots.|Мы решили этого не делать и обратно обьединить два участка. |Показываем экран с токенами.|
|12|We need to choose Merge in menu. Application will automaticaly check if there are land plots available for merge.|Выбираем пункт Обьединение в меню. Приложение автоматически проверяет, какие из участков можно объединить.|Нажимаем merge. Нажимаем merge у токена, который мы обьединяем.|
|13|Merge operation is done. You can perform same operations for building area tokens. For more information watch further videos, test sotware, read whitepaper and join us on telegram!|Операция обьединения выполнена. Эти операции так же можно применять к площадям зданий.|Показываем карту, потом облако точек, потом ссылки на группы.|


## Key Features - Real Estate operations on Ethereum

|№|English text|Russian text|Screen Action|
|------|-------|----------|-------|
|1|Ok, lets talk about the most interesting part of platform - trading.|----------|Показываем окно с токенами|
|2|In Galt Project you can trade your land or real estate ERC721 tokens for Ether, Stable Coins or any ERC20 tokens using smart contracts.|----------|Показываем окно с токенами|
|3|Of course if you want to buy or sell land or real estate on Ethereum you need to interact with the different legal systems and state institutions. |----------|Показываем окно с токенами|
|4|We provide 3 options to do that. In First option Buyer and Seller use government agency as a notary. Government agency on the basis of a smart contract registers ownership in the government property registry and approves escrow. This can be done automatically. |----------|Показываем окно с токенами|
|5|In Second option Buyer and Seller use Decentralized Custodians service. Custodians are organisations (Asset management companies or Trust funds) in reliable jurisdictions. They are temporary owners of land or real estate and are legally obliged to re-register these rights in the state registry to the owner of the token. Also they can convert fiat income from real estate to Ether or stable coins and transfer them to token owners. |----------|Показываем окно с токенами|
|6|In Third option Seller becomes a Custodian for Buyer. We will talk about all options in details in further videos.|----------|Показываем окно с токенами|
|7|In this video I will show, how i can sell my land plot or real estate token with Custodians service. I want to sell my vineyards. Absolutely like that, I can sell house, appartment or office. |----------|Показываем окно с токенами|
|8|I have 2 Custodians for my land plot. One company is based in Switzerland and the other one in Singapore. |----------|Нажимает на каждого из кастодианов. Должны быть человеческая информация: Название, адрес, Сайт , Government Registration number. Нужно подготовить реальные данные.|
|9|I will create a market order in token menu.|---|Нажимаем кнопку поставить на рынок.|
|10|I need to choose Ether or any other ERC20 token as payment, selling price.....let's make it 2000 ether, and ammount of contract fee. Also I can attach any legal or commercial documents in IPFS.|---|Нажимаем кнопку поставить на рынок.|
|11|Transaction is signed and confirmed and we can see our sale order.|---|Показываем заказ на продажу в меню|
|12|Bob wants to buy my vineyard for Ether. He can see my land plot here. He sees price, custodians information, commercial and legal documents.||Показываем раздел покупки и наш токен. Показываем кастодианов и документы.|
|13|Bob doesn't want to pay 2000 Ether. He thinks, that a good price is 1700. He makes a bid..... And we can see his offer here. Anytime Bob can change his bid.||Показываем, как Боб делает предложение.|
|14|Alice is also interested in my vineyard. She is ok to pay 1800 Ether. ||Показываем, как Элис делает предложение.|
|15|I don't like both offers, but i can make small discount. I change selling price for Alice and Bob to 1900 ether. ||Показываем, как я меняю цену для обоих предложений.|
|16|Now Alice is ok with my price. She changes her offer.||Показываем, как Алиса меняет цену.|
|17|When ask and bid prices are equal, I can select her offer and transfer my land plot token to escrow contract. Now I can withdraw my token back. But if Alice makes her payment, I wont be able to do that.||Принимаем предложение и отправляем токен на контракт.|
|18|Alice sends her payment.||Показываем, как отправляется оплата.|
|19|After both land plot token and ether were transfered to smart contract, both parties can confirm the deal or make a cancellation request. Cancellation requests are reviewed by the oracles community. But now everything is ok. And me and Alice confirm the deal. ||Показываем, как отправляется оплата. Показываем кнопку отмены и подтверждаем сделку обеими сторонами.|
|20|Alice can withdraw her brand new vineyard ERC721 Token.||Показываем, как выводится токен участка.|
|21|Аnd I can get my 1900 Ether.||Показываем, как беру оплату|
|22|Land and real estate trading on Ethereum is super fast, secure and reliable. You can buy and sell land, houses, appartment and offices in few clicks. With reliable international custodians, you don't need to think about local laws or due diligence||ПОказываем экран токенов|
|23|For more information watch further videos, test sotware, read whitepaper and join us on telegram! Like our video on youtube and join our channel.||Экран с токенами|
