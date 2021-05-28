# learningdatabase

# task 1

CREATE DATABASE hotel

CREATE TABLE hotel.customer (
    id int(4) NOT NULL,
    id_card_number varchar(16) NULL,
    name varchar(255) NULL,
    place_of_birth varchar(255) NULL,
    date_of_birth date NULL,
    gender varchar(1) NULL,
    address varchar(255) NULL,
    CONSTRAINT customer_pk PRIMARY KEY (id)
);

CREATE TABLE hotel.room_category (
    id int(4) NOT NULL,
	name varchar(15) NULL,
    description varchar(255) NULL,
    active TINYINT(1) NULL,
	created_by varchar(15) NULL,
	created_at timestamp NULL,
	CONSTRAINT room_category_pk PRIMARY KEY (id)
);

CREATE TABLE hotel.room_type (
    id int(4) NOT NULL,
    room_category_id int(4) NOT NULL,
    name varchar(15) NULL,
    description varchar(255) NULL,
    active TINYINT(1) NULL,
    created_by varchar(255) NULL,
    created_at timestamp NULL,
    CONSTRAINT room_type_pk PRIMARY KEY (id)
);

ALTER TABLE hotel.room_type ADD CONSTRAINT room_type_fk FOREIGN KEY (room_category_id) REFERENCES room_category(id);

CREATE TABLE hotel.stock_room (
    id int(4) NOT NULL,
    room_type_id int(4) NOT NULL,
    stock_total int(4) NULL,
    stock_available int(4) NULL,
    stock_ordered int(4) NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    updated_by varchar(15) NULL,
    updated_at timestamp NULL,
    CONSTRAINT stock_room_pk PRIMARY KEY (id)
);

ALTER TABLE hotel.stock_room ADD CONSTRAINT stock_room_fk FOREIGN KEY (room_type_id) REFERENCES room_type(id);

CREATE TABLE hotel.price_room (
	id int(4) NOT NULL,
    room_type_id int(4) NOT NULL, 
    price float(8) NULL,
	discount float(8) NULL,
    updated_by varchar(15) NULL,
    updated_at timestamp NULL,
	CONSTRAINT price_room_pk PRIMARY KEY (id) 
);

ALTER TABLE hotel.price_room ADD CONSTRAINT price_room_fk FOREIGN KEY (room_type_id) REFERENCES room_type(id);

CREATE TABLE hotel.transaction_history ( 
    id int(4) NOT NULL,
    number varchar(15) NULL,
    customer_id int(4) NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    CONSTRAINT transaction_history_pk PRIMARY KEY (id)
);

ALTER TABLE hotel.transaction_history ADD CONSTRAINT transaction_history_fk FOREIGN KEY (customer_id) REFERENCES customer(id);

CREATE TABLE hotel.transaction_history_detail (
    id int(4) NOT NULL,
    transaction_history_id int(4) NULL,
    room_type_id int(4) NULL,
    room_ordered int(4) NULL,
    quantity int(4) NULL,
    price int(4) NULL,
    created_by varchar(15) NULL,
    created_at timestamp NULL,
    updated_by varchar(15) NULL,
    updated_at timestamp NULL,
    CONSTRAINT transaction_history_detail_pk PRIMARY KEY (id)
);

ALTER TABLE hotel.transaction_history_detail ADD CONSTRAINT transaction_history_detail_fk FOREIGN KEY (transaction_history_id) REFERENCES transaction_history(id);

ALTER TABLE hotel.transaction_history_detail ADD CONSTRAINT transaction_history_detail_fk_1 FOREIGN KEY (room_type_id) REFERENCES room_type(id);