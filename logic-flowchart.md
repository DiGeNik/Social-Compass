```mermaid
graph TD
    %% Дефиниции на цветовете (Висок Контраст, Удебелен Текст)
    classDef startEnd fill:gold,stroke:#333,stroke-width:2px,font-weight:bold,color:black;
    classDef function fill:cornflowerblue,stroke:#333,stroke-width:2px,font-weight:bold,color:black;
    classDef io fill:lightgreen,stroke:#333,stroke-width:2px,font-weight:bold,color:black;
    classDef condition fill:salmon,stroke:#333,stroke-width:2px,font-weight:bold,color:black;
    classDef junction fill:#fff,stroke:#333,stroke-width:2px;

    %% Начало
    A(НАЧАЛО) --- J_Loop(( ));
    class A startEnd;
    class J_Loop junction;

    %% Съединител на главния цикъл
    J_Loop --- B[Таймерът стартира / Кортизол се увеличава +5 на всеки 5 мин];
    class B function;
    
    B --- C{Таймерът достига 45 мин?};
    class C condition;
    
    C ---|<b>"НЕ"</b>| J_Loop;
    C ---|<b>"ДА"</b>| E[СТОП ТАЙМЕР];
    class E function;

    %% Разклонение
    E --- F[/Показва &quot;Крузо Аларм&quot; с ФВС Мисия/];
    F --- G{Избор на потребител?};
    class F io;
    class G condition;

    %% Път 1: Изпълнение
    G ---|<b>"'Изпълних Мисията!'"</b>| H[Прилага &quot;Награда&quot;:<br>Кортизол -15<br>Ендорфини +20<br>Проверка: Ако < 0, задай на 0];
    H --- I[/Показва &quot;Браво!&quot;/];
    I --- J_Reset(( ));
    class H function;
    class I io;
    class J_Reset junction;

    %% Път 2: Отказ
    G ---|<b>"'Отказвам'"</b>| K[/Показва &quot;Етичен Филтър&quot; &#40;6 въпроса&#41;/];
    K --- L[/Изпращане на отговори/];
    L --- M{Отговори &apos;Да&apos; >= 3 ?};
    class K,L io;
    class M condition;

    %% Път 2A: Нисък риск
    M ---|<b>"НЕ &#40;Нисък риск&#41;"</b>| N[Прилага &quot;Наказание&quot;:<br>Ендорфини -20<br>Проверка: Ако < 0, задай на 0<br>Кортизол: БЕЗ ПРОМЯНА];
    N --- J_Reset;
    class N function;

    %% Път 2B: Висок риск
    M ---|<b>"ДА &#40;Висок риск&#41;"</b>| O[/Показва &quot;Кризисен Панел&quot;/];
    O --- P[/Натиска &quot;Разбрах&quot;/];
    P --- N;
    class O,P io;

    %% Събиране и Нулиране
    J_Reset --- Z[НУЛИРАНЕ НА ТАЙМЕР];
    class Z function;
    Z --- J_Loop;
```
