# SQL 테이블 생성
### Table - 'rec_cust'
        CREATE TABLE `rec_cust`
        (
        `cust_id` VARCHAR(30) NOT NULL
        COMMENT '고객아이디',
        `cust_nm` VARCHAR(20) NOT NULL
        COMMENT '고객명',
        `gender` VARCHAR(1) NOT NULL
        COMMENT '성별',
        `birth` VARCHAR(8) NOT NULL
        COMMENT '출생연도',
        `cell_no` VARCHAR(20)
        COMMENT '휴대폰번호',
        `ap_path_cd` VARCHAR(3) NOT NULL
        COMMENT '가입경로구분코드',
        `data_input_time` DATE NOT NULL
        COMMENT '데이터입력일시',
        `data_input_nm` VARCHAR(30) NOT NULL
        COMMENT '데이터입력자',
        `data_mod_time` DATE NOT NULL
        COMMENT '데이터수정일시',
        `data_mod_nm` VARCHAR(30) NOT NULL
        COMMENT '데이터수정자'
        )
        COMMENT = '고객';
        ALTER TABLE `rec_cust`
        ADD CONSTRAINT `엔터티1_PK` PRIMARY KEY
        ( `cust_id` );


### Table - 'rec_pur'
        CREATE TABLE `rec_pur`
        (
        `cust_id` VARCHAR(30) NOT NULL
        COMMENT '고객아이디',
        `pd_id` VARCHAR(30) NOT NULL
        COMMENT '상품아이디',
        `data_input_time` DATE NOT NULL
        COMMENT '데이터입력일시',
        `data_input_nm` VARCHAR(30) NOT NULL
        COMMENT '데이터입력자'
        )
        COMMENT = '구매';
        ALTER TABLE `rec_pur`
        ADD CONSTRAINT `엔터티1_PK2` PRIMARY KEY
        ( `cust_id`,`pd_id` );


### Table - 'rec_pd'
        CREATE TABLE `rec_pd`
        (
        `pd_id` VARCHAR(30) NOT NULL
        COMMENT '상품아이디',
        `pd_nm` VARCHAR(100) NOT NULL
        COMMENT '상품명',
        `pd_dtl_cont` Text NOT NULL
        COMMENT '상품상세내용',
        `pd_img` BLOB NOT NULL
        COMMENT '상품이미지',
        `data_input_time` DATE NOT NULL
        COMMENT '데이터입력일시',
        `data_input_nm` VARCHAR(30) NOT NULL
        COMMENT '데이터입력자'
        )
        COMMENT = '상품';
        ALTER TABLE `rec_pd`
        ADD CONSTRAINT `엔터티1_PK1` PRIMARY KEY ( `pd_id` );


# 데이터 삽입
    
    INSERT INTO `rec_cust`(`cust_id`, `cust_nm`, `gender`, `birth`, `cell_no`, `ap_path_cd`, `data_input_time`, `data_input_nm`, `data_mod_time`, `data_mod_nm`)
    VALUES ('ID01', 'jane', '2', '19800101','010-0000-0000', 'P01', NOW(), 'system', NOW(), 'system'),
    ('ID02', 'Kelly', '2', '19800102','010-0000-0000', 'P02', NOW(), 'system', NOW(), 'system'),
    ('ID03', 'June', '1', '19800103','010-0000-0000', 'P01', NOW(), 'system', NOW(), 'system')
    ;

    INSERT INTO `rec_pd`(`pd_id`, `pd_nm`, `pd_dtl_cont`, `pd_img`, `data_input_time`, `data_input_nm`)
    VALUES ('PD01', '3분카레', '3분안에 만들수 있는카레', '', NOW(), 'system'),
    ('PD02', '미트볼', '미트볼 소스는 미트미트', '', NOW(), 'system'),
    ('PD03', '함박세트', '부드러운 맛이 일품인', '', NOW(), 'system')
    ;

    INSERT INTO `rec_pur`(`cust_id`, `pd_id`, `data_input_time`, `data_input_nm`)
    VALUES ('ID01', 'PD01', NOW(), 'system'),
    ('ID03', 'PD01', NOW(), 'system'),
    ('ID03', 'PD03', NOW(), 'system')
    ;


# SQL 검색

### rec_pd 모든 테이블 정보 탐색
- select * from rec_pd ;

### rec_pur 테이블에서 cust_Id, pd_id,Count(1) 검색 (cust_id, pd_id를 그룹화)
SELECT cust_id, pd_id, COUNT(1)
FROM `rec_pur`
GROUP BY cust_id, pd_id
;