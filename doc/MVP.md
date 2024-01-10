# MVP of AsciiArtify

0. На попередніх етапах було налаштовано зв'язку k3d та ArgoCD. Тому використаємо її та додамо у наш існуючий кластер сам додаток від AsciiArtify.
1. Додаток візьмемо у нашого ментора den-vasyliev/go-demo-app , зробивши fork.
2. У ArgoCD GUI додамо новий додаток, натиснувши "+NEW APP", вкажемо наступні параметри, як на скрінах: 
<img width="750" alt="1_agro_newapp" src="https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/15f9cdb3-bd29-4e2e-8a36-08af6273dc7a">

- У розділі `SOURCE` тип джерела залишаємо за замовчуванням `GIT`
- Введемо `url` репозиторію, який містить маніфести для розгортання https://github.com/sbazanov/go-demo-app (це буде helm charts, або пакет маніфестів який являє собою групу об'єктів для Kubernetes та нашого додатку)
- У полі `Path` введемо шлях до каталогу `helm`
![2_argo_helm](https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/242e5c5f-0a8f-4a60-af67-83a183bd7477)

- В розділі `DESTINATION` вкажемо `url` локального кластеру та `Namespace` demo після чого ArgoCD автоматично визначить параметри додатку використавши маніфести, які знаходяться в репозиторії. В разі бажання змінити значення вручну можна змінити іх значення в розділі `PARAMETERS`. 
<img width="732" alt="3_argo_dest" src="https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/5aef44b7-b197-4c12-9372-84998c022100">

- У розділі політика синхронізація вкажемо як додаток буде синхронізуватись з репозиторієм. Тут важливо вказати ArgoCD щоб створив новий namespace так як в helm цю функцію за замовчуванням прибрали. Ставимо галку напроти `AUTO-CREATE NAMESPACE`   
- Створюємо додаток кнопкою `CREATE`

3. Налаштуємо мапування портів для застосунку AsciiArtify
```bash
$ k port-forward -n demo svc/ambassador 8081:80&
Forwarding from 127.0.0.1:8081 -> 80
Forwarding from [::1]:8081 -> 80
```
- Перевіремо мапування:  
```bash
$ curl localhost:8081
k8sdiy-api:931d5e8#       
```
4. Перевіримо роботу застосунка, а саме конвертацію графічного файлу у ascii 
- Для цього завантажимо файл що зберігається у нас в локальному сховищі на вітдалений сервер командою:
```bash
curl -F 'image=@250px-Flag_of_Ukraine.svg.png' localhost:8081/img/
```
- Результат в консолі:
![AsciiArtify_result](https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/d7b788e0-9d18-4e33-85c7-e29bcc9248bc)

***Відео-інструкція:***

https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/aba29501-3bbe-417f-80eb-ecabe430c94e


  
    

