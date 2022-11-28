# SQL-Average-revenue-per-user
Using SQL to find the ARPU

     select *
     from purchases
     LIMIT 5;

     select *
     from gameplays
     LIMIT 5;
     
![image](https://user-images.githubusercontent.com/39978937/204189394-6708da2e-f950-4698-87ea-be67f150f9ae.png)



--------------------------------------------------------------------------------------------------------------------------------

    with daily_revenue as (
      
      select
        date(created_at) as dt,
        round(sum(price), 2) as rev
      from purchases
      where refunded_at is null
      group by 1
    ), 
    
    daily_players as (
      select
        date(created_at) as dt,
        count(distinct user_id) as players
      from gameplays
      group by 1
    )
    
    select
      daily_revenue.dt,
      daily_revenue.rev / daily_players.players
    from daily_revenue
      join daily_players using (dt);


![image](https://user-images.githubusercontent.com/39978937/204189209-7772af18-e6ce-4cd1-9341-1c108817dc4a.png)
