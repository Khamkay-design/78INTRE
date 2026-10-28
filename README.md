# 78win
78WIN - Gaming Platform | Tic-Tac-Toe + Rock-Paper-Scissors with Leaderboard, User Profile &amp; 

-- User preferences: each user accesses only their own settings.
drop policy if exists preferences_select_own
  on public.user_preferences;

create policy preferences_select_own
on public.user_preferences
for select to authenticated
using ((select auth.uid()) = user_id);

drop policy if exists preferences_insert_own
  on public.user_preferences;

create policy preferences_insert_own
on public.user_preferences
for insert to authenticated
with check ((select auth.uid()) = user_id);

drop policy if exists preferences_update_own
  on public.user_preferences;

create policy preferences_update_own
on public.user_preferences
for update to authenticated
using ((select auth.uid()) = user_id)
with check ((select auth.uid()) = user_id);

-- Support tickets: users can read and create their own tickets.
drop policy if exists tickets_select_own
  on public.support_tickets;

create policy tickets_select_own
on public.support_tickets
for select to authenticated
using ((select auth.uid()) = user_id);

drop policy if exists tickets_insert_own
  on public.support_tickets;

create policy tickets_insert_own
on public.support_tickets
for insert to authenticated
with check ((select auth.uid()) = user_id);

commit;
