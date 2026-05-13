# pwr-wash-profit
Project profitability analysis app
create table if not exists employees (
  id text primary key,
  name text not null,
  rate numeric not null,
  created_at timestamptz default now()
);

create table if not exists projects (
  id text primary key,
  name text not null,
  type text,
  factura numeric default 0,
  month integer,
  status text default 'active',
  otros jsonb default '[]',
  created_at timestamptz default now()
);

create table if not exists entries (
  id text primary key,
  project_id text references projects(id),
  date text not null,
  nomina jsonb default '[]',
  gas numeric default 0,
  otros numeric default 0,
  note text default '',
  created_at timestamptz default now()
);

alter table employees enable row level security;
alter table projects  enable row level security;
alter table entries   enable row level security;

create policy "public_all_employees" on employees for all using (true) with check (true);
create policy "public_all_projects"  on projects  for all using (true) with check (true);
create policy "public_all_entries"   on entries   for all using (true) with check (true);
