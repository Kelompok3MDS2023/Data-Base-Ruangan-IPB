# Data-Base-Ruangan-IPB

Merancang ERD dan membuat database 

Tabel Fakultas
```sql
CREATE TABLE IF NOT EXISTS public.fakultas (
    Kode_Fk character varying(2) NOT NULL,
    Nm_Fk text NOT NULL,
    Jml_Prodi integer NOT NULL,
    PRIMARY KEY (Kode_Fk)
);
```

Tabel Ruangan

```sql
CREATE TABLE IF NOT EXISTS public.ruangan (
    Kode_RG character varying(25) NOT NULL,
    Nm_RG text NOT NULL,
    Lokasi text NOT NULL,
    Kapasitas integer NOT NULL,
    PRIMARY KEY (Kode_RG)
);
```

Jadwal Kuliah
```sql
CREATE TABLE IF NOT EXISTS public.Jadwal_Kuliah (
    Kode_MK character varying(10) NOT NULL,
    Jadwal text NOT NULL,
    Peserta integer NOT NULL,
    PRIMARY KEY (Kode_MK)
);
```

Mata Kuliah
```sql
CREATE TABLE IF NOT EXISTS public.Mata_Kuliah (
    Kode_MK character varying(10) NOT NULL,
    Nm_MK text NOT NULL,
    Semester integer NOT NULL,
    PRIMARY KEY (Kode_MK)
);
```

Ruangan di Fakultas
```sql
CREATE TABLE IF NOT EXISTS public.ruangan_di_fakultas(
    Kode_Fk character varying(2) COLLATE pg_catalog."default" NOT NULL,
    Kode_RG character varying(25) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT ruangan_di_fakultas_pkey PRIMARY KEY (Kode_Fk , Kode_RG),
    CONSTRAINT ruangan_di_fakultas_Kode_Fk_fkey FOREIGN KEY (Kode_Fk)
        REFERENCES public.fakultas (Kode_Fk) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT ruangan_di_fakultas_Kode_RG_fkey FOREIGN KEY (Kode_RG)
        REFERENCES public.ruangan (Kode_RG) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
);
```

Ruangan_Mk
```sql
CREATE TABLE IF NOT EXISTS public.ruangan_mk(
    Kode_RG character varying(25) COLLATE pg_catalog."default" NOT NULL,
    Kode_MK character varying(10) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT ruangan_mk_pkey PRIMARY KEY (Kode_RG,Kode_MK),
    CONSTRAINT ruangan_mk_fkey FOREIGN KEY (Kode_RG)
        REFERENCES public.ruangan (Kode_RG) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT ruangan_mk_fkey FOREIGN KEY (Kode_MK)
        REFERENCES public.Jadwal_Kuliah (Kode_MK) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
);
```

Jadwal_untuk_MK
```sql
CREATE TABLE IF NOT EXISTS public.Jadwal_untuk_MK(
    Kode_MK character varying(10) COLLATE pg_catalog."default" NOT NULL,
    Kode_MK character varying(10) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT Jadwal_untuk_MK_pkey PRIMARY KEY (Kode_MK,Kode_MK),
    CONSTRAINT Jadwal_untuk_MK_fkey FOREIGN KEY (Kode_MK)
        REFERENCES public.Jadwal_Kuliah (Kode_MK) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT Jadwal_untuk_MK_fkey FOREIGN KEY (Kode_MK)
        REFERENCES public.Mata_Kuliah (Kode_MK) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
);
```
