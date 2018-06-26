FROM library/postgres:9.6.9

RUN printf "max_connections = 200\nshared_buffers = 7680MB\neffective_cache_size = 23040MB\nmaintenance_work_mem = 1920MB\ncheckpoint_completion_target = 0.7\nwal_buffers = 16MB\ndefault_statistics_target = 100\nrandom_page_cost = 1.1\neffective_io_concurrency = 200\nwork_mem = 393kB\nmin_wal_size = 1GB\nmax_wal_size = 2GB\nmax_worker_processes = 8\nmax_parallel_workers_per_gather = 4\n" >> /usr/share/postgresql/postgresql.conf.sample

ENV POSTGRES_USER flow_bakery_user
ENV POSTGRES_PASSWORD flow_bakery_user_pw_t221w
ENV POSTGRES_DB flow_bakery
EXPOSE 5432
