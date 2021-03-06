1.  В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения** и выберите узел **Обновления программного обеспечения**.  

2.  Выберите необходимое для загрузки программное обеспечение одним из следующих способов.  

    -   В узле **Группы обновлений программного обеспечения** выберите одну или несколько групп обновлений программного обеспечения. На ленте нажмите кнопку **Загрузить**.  

    -   В узле **Все обновления программного обеспечения** выберите одно или несколько обновлений программного обеспечения. На ленте нажмите кнопку **Загрузить**.  

        > [!NOTE]  
        >  В узле **Все обновления программного обеспечения** Configuration Manager отображает только обновления классификаций **Критическое** и **Безопасность**, а также обновления, выпущенные за последние 30 дней.  

        > [!TIP]  
        >  Нажмите кнопку **Добавить условие**, чтобы отфильтровать обновления программного обеспечения, которые отображаются в узле **Все обновления программного обеспечения**. Сохраните часто используемые поисковые запросы и начните управлять сохраненными результатами поиска на вкладке **Поиск**.  


3.  На странице **Пакет развертывания** мастера загрузки обновлений программного обеспечения настройте приведенные ниже параметры.  

    -  **Выбор пакета развертывания**: этот параметр используется для выбора существующего пакета развертывания для развертываемых обновлений программного обеспечения.  

        > [!NOTE]  
        >  Обновления программного обеспечения, которые сайт уже загрузил в выбранный пакет развертывания, повторно не загружаются.  

    -  **Создание нового пакета развертывания**: этот параметр используется для создания нового пакета развертывания для развертываемых обновлений программного обеспечения. Настройте следующие параметры.  

        -   **Имя**: задает имя пакета развертывания. Пакет должен иметь уникальное имя, кратко описывающее содержимое пакета. Его длина ограничена 50 символами.  

        -   **Описание**: укажите описание, содержащее сведения о пакете развертывания. Длина необязательного описания ограничена 127 символами.    

        -   **Исходные файлы пакета**: расположение исходных файлов обновления программного обеспечения. Введите сетевой путь к каталогу с исходными файлами (например, `\\server\sharename\path`) или выберите его с помощью кнопки **Обзор**. Перед переходом на следующую страницу создайте общую папку для исходных файлов пакета развертывания.  

             - Указанное расположение нельзя использовать в качестве источника другого пакета развертывания программного обеспечения.  

             - Местоположение источника пакета можно изменить в свойствах пакета развертывания после того, как Configuration Manager создаст пакет развертывания. В этом случае необходимо сначала скопировать содержимое из исходного расположения оригинального пакета в новое расположение источника пакета.  

             -  Учетной записи компьютера поставщика SMS и пользователю, работающему с мастером загрузки обновлений программного обеспечения, требуются разрешения на **запись** в папку загрузки. Ограничьте доступ к папке загрузки. Это ограничение позволяет снизить риск подмены злоумышленниками исходных файлов обновлений программного обеспечения.  

        - **Использовать двоичную дифференциальную репликацию**: включите этот параметр, чтобы свести к минимуму сетевой трафик между сайтами. Двоичная дифференциальная репликация (BDR) обновляет только содержимое, которое изменилось в пакете, и не обновляет содержимое всего пакета. Дополнительные сведения см. в разделе [Двоичная дифференциальная репликация](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  На странице **Точки распространения** укажите точки распространения или группы точек распространения для размещения файлов обновления программного обеспечения. Дополнительные сведения о точках распространения см. в разделе [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Этот страница доступна только при создании нового пакета развертывания обновлений программного обеспечения.  

5.  Страница **Точки распространения** доступна только при создании пакета развертывания обновлений программного обеспечения. Укажите следующие параметры.  

    -   **Приоритет распространения**: используйте этот параметр, чтобы указать приоритет распространения для пакета развертывания. Приоритет распространения применяется в случае отправки пакета развертывания в точки развертывания, расположенные на дочерних сайтах. Передача пакетов развертывания осуществляется в порядке приоритета: "Высокий", "Средний" и "Низкий". Пакеты с одинаковым приоритетом передаются в том порядке, в котором они были созданы. Если очередь пакетов отсутствует, обработка пакета выполняется незамедлительно, причем независимо от уровня приоритета. По умолчанию сайт отправляет пакеты с приоритетом **Средний**.  

    -   **Enable for on-demand distribution** (Включить для распространения по запросу): используйте этот параметр, чтобы включить распространение содержимого по запросу в точках распространения, настроенных для этой функции, и в текущей группе границ клиента. При включении этого параметра точка управления создает триггер для диспетчера распространения. Содержимое распространяется на все точки распространения в тех ситуациях, когда клиент запрашивает содержимое пакета, а оно оказывается недоступным. Дополнительные сведения см. в разделе [Распространение содержимого по запросу](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Параметры предварительно подготовленной точки распространения**: используйте этот параметр, чтобы указать способы распространения содержимого на предварительно подготовленные точки распространения. Выберите один из следующих вариантов.  

        -   **Автоматически загружать содержимое при назначении пакетов точкам распространения**: используйте этот параметр, чтобы не использовать параметры предварительной подготовки и распространять содержимое в точку распространения.   

        -   **Загружать в точку распространения только изменения содержимого**: используйте этот параметр, чтобы предварительно скопировать содержимое в точку распространения, а затем распространить изменения содержимого в точку распространения.  

        -   **Вручную копировать содержимое этого пакета в точку распространения**: используйте этот параметр, чтобы всегда предварительно подготавливать содержимое в точке распространения. Это значение по умолчанию.  

        Дополнительные сведения о предварительной подготовке содержимого в точках распространения см. в разделе [Об использовании предварительно подготовленного содержимого](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  На странице **Расположение загрузки** укажите расположение, используемое Configuration Manager для загрузки исходных файлов обновления программного обеспечения. Используйте один из следующих вариантов:  

    -   **Загружать обновления программного обеспечения из Интернета**: выберите этот параметр, чтобы загружать обновления программного обеспечения из Интернета. Это значение по умолчанию.  

    -   **Загружать обновления программного обеспечения из расположения в моей сети**: выберите этот параметр, чтобы загружать обновления программного обеспечения из локальной папки или общей папки. Выберите этот параметр, если компьютер, на котором выполняется мастер, не имеет доступа к Интернету. На любом компьютере с доступом к Интернету поддерживается предварительная загрузка обновлений программного обеспечения. Затем сохраните обновления в папке в локальной сети, доступной с компьютера, на котором запущен мастер.  


7.  На странице **Выбор языка** выберите языки, для которых сайт загружает выбранные обновления программного обеспечения. Сайт загружает обновления программного обеспечения только в том случае, если они доступны на выбранных языках. Обновления программного обеспечения, не зависящие от языка, загружаются в любом случае. По умолчанию мастер выбирает языки, настроенные вами в свойствах точки обновления программного обеспечения. Перед переходом к следующей странице необходимо выбрать по крайней мере один язык. Если ни один из выбранных языков не поддерживается обновлением, оно не загружается.  

8. На странице **Сводка** проверьте выбранные в мастере параметры, а затем нажмите кнопку **Далее**, чтобы загрузить обновления программного обеспечения.  

9. На странице **Завершение** убедитесь в успешной загрузке обновлений программного обеспечения и нажмите кнопку **Закрыть**.  
