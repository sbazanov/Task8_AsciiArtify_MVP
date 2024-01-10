# MVP of AsciiArtify

0. На попередніх етапах було налаштовано зв'язку k3d та ArgoCD. Тому використаємо її та додамо у наш існуючий кластер сам додаток від AsciiArtify.
1. Додаток візьмемо у нашого ментора den-vasyliev/go-demo-app , зробивши fork.
2. У ArgoCD GUI додамо новий додаток, натиснувши "+NEW APP", вкажемо наступні параметри, як на скрінах: 
<img width="750" alt="1_agro_newapp" src="https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/15f9cdb3-bd29-4e2e-8a36-08af6273dc7a">

- У розділі `SOURCE` тип джерела залишаємо за замовчуванням `GIT`
- Введемо `url` репозиторію, який містить маніфести для розгортання https://github.com/sbazanov/go-demo-app (це буде helm charts, або пакет маніфестів який являє собою групу об'єктів для Kubernetes та нашого додатку)
- У полі `Path` введемо шлях до каталогу `helm`  
![2_argo_helm](https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/318903ae-40c7-4aef-a581-bfc161ac89c6)

- В розділі `DESTINATION` вкажемо `url` локального кластеру та `Namespace` demo після чого ArgoCD автоматично визначить параметри додатку використавши маніфести, які знаходяться в репозиторії. В разі бажання змінити значення вручну можна змінити іх значення в розділі `PARAMETERS`. 
<img width="732" alt="3_argo_dest" src="https://github.com/sbazanov/Task8_AsciiArtify_MVP/assets/96147501/5aef44b7-b197-4c12-9372-84998c022100">



     
