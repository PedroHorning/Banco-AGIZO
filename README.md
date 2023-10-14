# Banco-AGIZO

CREATE DATABASE curriculo;

CREATE TABLE IF NOT EXISTS public.cabecalho
(
    id integer NOT NULL DEFAULT nextval('cabecalho_id_seq'::regclass),
    nome character varying(255) COLLATE pg_catalog."default",
    idade integer,
    cidade character varying(255) COLLATE pg_catalog."default",
    id_curriculo integer,
    CONSTRAINT cabecalho_pkey PRIMARY KEY (id)
)

CREATE TABLE IF NOT EXISTS public.curriculo
(
    id integer,
    id_usuario integer,
    id_cabecalho integer,
    resumo_profissional text COLLATE pg_catalog."default",
    id_experiencia integer,
    id_formacao integer,
    id_habilidade integer,
    CONSTRAINT fk_curriculo_experiencia FOREIGN KEY (id_experiencia)
        REFERENCES public.experiencia (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT fk_curriculo_formacao FOREIGN KEY (id_formacao)
        REFERENCES public.formacao (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT fk_curriculo_habilidade FOREIGN KEY (id_habilidade)
        REFERENCES public.habilidade (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

CREATE TABLE IF NOT EXISTS public.experiencia
(
    id integer NOT NULL DEFAULT nextval('experiencia_id_seq'::regclass),
    cargo character varying(255) COLLATE pg_catalog."default",
    data_inicio date,
    data_fim date,
    descricao text COLLATE pg_catalog."default",
    id_curriculo integer,
    CONSTRAINT experiencia_pkey PRIMARY KEY (id)
)

CREATE TABLE IF NOT EXISTS public.formacao
(
    id integer NOT NULL DEFAULT nextval('formacao_id_seq'::regclass),
    curso character varying(255) COLLATE pg_catalog."default",
    data_inicio date,
    data_fim date,
    descricao text COLLATE pg_catalog."default",
    local character varying(255) COLLATE pg_catalog."default",
    id_curriculo integer,
    CONSTRAINT formacao_pkey PRIMARY KEY (id)
)

CREATE TABLE IF NOT EXISTS public.habilidade
(
    id integer NOT NULL DEFAULT nextval('habilidade_id_seq'::regclass),
    descricao character varying(255) COLLATE pg_catalog."default",
    nivel character varying(255) COLLATE pg_catalog."default",
    id_curriculo integer,
    CONSTRAINT habilidade_pkey PRIMARY KEY (id)
)

CREATE TABLE IF NOT EXISTS public.usuario
(
    id integer NOT NULL DEFAULT nextval('usuario_id_seq'::regclass),
    nome character varying(255) COLLATE pg_catalog."default",
    tipo character varying(50) COLLATE pg_catalog."default",
    email character varying(255) COLLATE pg_catalog."default",
    senha character varying(255) COLLATE pg_catalog."default",
    CONSTRAINT usuario_pkey PRIMARY KEY (id),
    CONSTRAINT usuario_email_key UNIQUE (email)
)
