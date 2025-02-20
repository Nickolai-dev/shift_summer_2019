# уязвимость/атака

## Описание

Insecure Direct Object Reference (небезопасные прямые ссылки на объекты) (IDOR) - Уязвимость подразумевает ситуацию, когда пользователь может успешно получить доступ к странице, данным или файлу, доступа к которым у него быть не должно.

## Классификация
- Атака влияет на сервер url запросом который может выполнить скрипт или вывести текст файла.

## Условия
- ОС: любая
- язык: любой
- компоненты: файлы пользователей
- настройки: разные

При использовании некоторых фреймворков (Django, Flask) уязвимость не проявляется. Прямое чтение файлов возможнотолько из папки static.

## Детектирование
	Детектировать уязвимость возможно:
	- На бэке не настроенны роуты
	- Отсутствует разрешение на просмотр папок 
	- Возможно прямое обращение к файлам в url (0.0.0.0:1338/news.txt)
	- Возможность получить данные (например, данные другого пользователя) при изменении параметров строки запроса
	- Отсутствие файла .htaccess или неправильная его настройка ( не во всех языках )	
## Эксплуатация
	Эксплуатация данной уязвимости очень проста и не требует вообще никаких специальных навыков – достаточно лишь перебирать введенные данные в адресной строке браузера. 

	Например, 
	заходим на сайт: http://172.16.53.124:1338/

	В конце сайта смотрим пользователей, берём любой логин и подставляем его http://172.16.53.124:1338/ddawdawd

	Теперь добавляем .txt : http://172.16.53.124:1338/ddawdawd.txt.
	Переходим по ссылке и получаем данные пользователя ddawdawd.

### Инструменты
	- *Эксплуатация данной уязвимости очень проста и не требует вообще никаких специальных навыков – достаточно лишь перебирать число в адресной строке браузера и наслаждаться результатом. *
## Ущерб
	- Возможность получения доступа к файлам (доступа к которым у них не должно быть) сторонними пользователям 	
	* - Возможность получения доступа к сессиям *
## Защита
### Основные меры
	- Настройка приватности файлов(например, с использованием настроек файла .htaccess)
	- Не хранить важные файлы в папках static (при использовании Flask)
	- Настройка роутинга
	- Настройка грамотной аутентификации и авторизации
	- Использования хэша 
### Превентивные меры
	подход Defense in Depth:
	- подвергать файлы шифрованию содержащие важную информацию 
## Дополнительно
	http://software-testing.ru/library/testing/security/2991-testing-for-idor-vulnerabilitie
