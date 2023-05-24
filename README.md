# Tech-Alchemy
Advanced Database Operations using SQLAlchemy

from sqlalchemy import create_engine,ForeignKey,Column,String,Integer,CHAR

from sqlalchemy.ext.declarative import declarative_base

from sqlalchemy.orm import sessionmaker

Base=declarative_base()

class Person(Base):
    __tablename__="people"

    ssn=Column("ssn",Integer,primary_key=True)
    firstname=Column("firstname",String)
    gender=Column("gender",CHAR)
    age=Column("age",Integer)

    def __init__(self,ssn,first,gender,age):
        self.ssn=ssn
        self.firstname=first
        self.gender=gender
        self.age=age

    def __repr__(self):
        return f"({self.ssn}){self.firstname}({self.gender},{self.age})"

class Thing(Base):
    __tablename__="things"

    tid=Column("tid",Integer,primary_key=True)
    description=Column("description",String)
    owner=Column(Integer,ForeignKey("people.ssn"))

    def __init__(self,tid,description,owner):
        self.tid=tid
        self.description=description
        self.owner=owner

    def __repr__(self):
        return f"({self.tid}) {self.description} owned by {self.owner}"

    

engine=create_engine("sqlite:///mydb.db",echo=True)

Base.metadata.create_all(bind=engine)

Session=sessionmaker(bind=engine)

session=Session()

person=Person(241019,"Bob","m",19)

session.add(person)

session.commit()


p1=Person(241027,"Danny","m",26)

p2=Person(241034,"Rocky","m",42)

p3=Person(241036,"Creed","m",45)

session.add(p1)

session.add(p2)

session.add(p3)

session.commit()

t1=Thing(1,"Car",p1.ssn)

t2=Thing(2,"Laptop",p1.ssn)

t3=Thing(3,"PS5",p2.ssn)

t4=Thing(4,"Tool",p3.ssn)

t5=Thing(5,"Book",p3.ssn)

session.add(t1)

session.add(t2)

session.add(t3)

session.add(t4)

session.add(t5)

session.commit()

#results=session.query(Person).all()

#results=session.query(Person).filter(Person.age>25)

#results=session.query(Person).filter(Person.firstname.like("%n"))

#results=session.query(Person).filter(Person.ssn.in_(["Bob","Rocky"]))


results=session.query(Thing,Person).filter(Thing.owner==Person.ssn).filter(Person.firstname=="Franclin").all()

for r in results:

    print(r)
