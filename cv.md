# RESUME

  
  

1. Gleb Kozlovky
2. e-mail: kozlovskij.gleb@mail.ru; phone: +375-(33)-671-27-43
3. EPAM is one of the leading it companies. RS-School allows you to gain knowledge in the field of web development, communicate with experts who work on projects. I am a hard-working and stress-resistant person, I have a burning passion for programming, and I am ready to work every day to reach new heights.
4. Middle level C++, beginner level in JavaScript / HTML / CSS.
5. - Develop a class hierarchy for a role-playing game
```
  class Personage
{
protected:
//Name
	string name;
//luck in the attack
	int luck_attack;
//luck in the guard
	int luck_guard;
//health
	int health=100;
//attack weapons
	Weapon * weapon_attack;
//the weapon of defense
	Weapon * weapon_guard;
	int p;
public:
	Personage(): name(0)
	{}
	Personage(string name): name(name)
	{}
	virtual void Attack(Personage* Personage) = 0;
	virtual void Guard(int a) {};
//false – игрок еще жив, иначе true
	bool IsDead() 
	{
		return (health <= 0); 
	}
//установить оружие атаки
	void SetWeaponAttack(Weapon* w)
	{
		

		weapon_attack = w;
		
	}
//установить оружие защиты
	void SetWeaponGuard(Weapon * w)
	{
		
		SetWeaponAttack();
		weapon_guard = w;
	}
};

class Weapon
{
public:
	int power;
	int guard;
	Weapon():power(power)
	{}
	Weapon(int power): power(power)
	{
	
	}



};
class Storm : public Weapon
{
public:
	Storm(): Weapon(30)
	{
	
	}
};
class Shield :public Weapon //щит
{
public:
		Shield(): Weapon(10)
		{}
};

class Club :public Weapon //дубинка
{public:
	Club() : Weapon(15)
	{}
};


class Warrior:public Personage, public Weapon
{
public:
	int p;
	Warrior(string name): Personage(name)
	{
		cout << "Warrior name " << this->name << endl;
	}
    void Attack(Personage* personage) override
    {
		int s=rand() % 3+1;
		if (s == 1)
		{
			
			Storm weapon;
			personage->SetWeaponAttack(&weapon);
		}
		else if (s == 2)
		{
			Shield weapon;
			personage->SetWeaponAttack(&weapon);
		}
		else
		{
			Club weapon;
			personage->SetWeaponAttack(&weapon);
		}
		luck_attack = rand() % weapon_attack->power / 2 + (-weapon_attack->power / 2);
		cout << "Warrior attack" << endl;
		p = luck_attack + weapon_attack->power;
		
    }
	void Guard(int a) override
	{

		int s = rand() % 3 + 1;
		if (s == 1)
		{
			Storm weapon;
			SetWeaponGuard(&weapon);
		}
		else if (s == 2)
		{
			Shield weapon;
			SetWeaponGuard(&weapon);
		}
		else
		{
			Club weapon;
			SetWeaponGuard(&weapon);
		}
		luck_guard = rand() % weapon_guard->power / 2 + (-weapon_guard->power / 2);
		health -= (a - luck_guard);
		cout << "Warrior guard" << endl;
		cout << "Warrior health " <<health<< endl;
	}
};


class Monster:public Personage, public Weapon
{
public:
	int p;
	Monster():Personage("")
	{}
	Monster(string name): Personage(name)
	{
		cout << "Monster name " << this->name << endl;
	}
	void Attack(Personage* personage) override
	{
		int s = rand() % 3 + 1;
		if (s == 1)
		{
			Storm weapon;
			personage->SetWeaponAttack(&weapon);
		}
		else if (s == 2)
		{
			Shield weapon;
			personage->SetWeaponAttack(&weapon);
		}
		else
		{
			Club weapon;
			personage->SetWeaponAttack(&weapon);
		}
		luck_attack = rand() % weapon_attack->power / 2 + (-weapon_attack->power / 2);
		cout << "Monster attack" << endl;
		p = luck_attack + weapon_attack->power;

	}
	void Guard(int a) override
	{
		
		int s = rand() % 3 + 1;
		if (s == 1)
		{
			Storm weapon;
			SetWeaponGuard(&weapon);
		}
		else if (s == 2)
		{
			Shield weapon;
			SetWeaponGuard(&weapon);
		}
		else
		{
			Club weapon;
			SetWeaponGuard(&weapon);
		}
		luck_guard = rand() % weapon_guard->power / 2 + (-weapon_guard->power / 2);
		health -= (a - luck_guard);
		cout << "Monster guard" << endl;
		cout <<"Monster health "<< health<<endl;
	}
};


int main()	
{
	srand(time(NULL));
	int q = 0;
	Warrior a("Alpha");
	Monster b("Beta");
	while (a.IsDead() == false && b.IsDead()==false)
	{
		if (q == 0) {
			a.Attack(&a);
			b.Guard(a.p);
			q++;
		}
		else
		{
			b.Attack(&b);
			a.Guard(b.p);
			q--;
		}
	
	}
	if (a.IsDead() == true)
	{
		cout << "Warrior dead";
	}
	else cout << "Monster dead;";


}
```
- Stack:
~~~
struct List
{
	int x;                                              
	List *Next;
}*Head;


void Add(int x)
{
	List *temp = new List;                             
	temp->x = x;                                        
	temp->Next = Head;                         
	Head = temp;                               
}


void Show()                                
{
	List *temp = Head;                          
	while (temp != NULL)                                
	{
		cout << temp->x<<' ';
		temp = temp->Next;                             
	}
}


void ShowOtr()
{
	List *temp = Head;
	while (temp != NULL)
	{
		if (temp->x < 0)
		{
			cout << "Negative element" << endl; 
			break;
		}
		else temp = temp->Next;
		
	}
}


void izm(List *max, List *min)
{
	List *maxs=Head;
	List *mins=Head;
	List *t;
	if (Head == max)  // Если максимальный элемент первый
	{
		while (mins->Next != min) mins = mins->Next;
		t = Head;
		Head = mins->Next;
		mins->Next = t;
		t = Head->Next;
		Head->Next = max->Next;
		mins->Next->Next = t;

	}
	else if (Head == min)  // Если минимальный элемент первый 
	{
		while (maxs->Next != max) maxs = maxs->Next;
		t = Head;
		Head = maxs->Next;
		maxs->Next = t;
		t = Head->Next;
		Head->Next = min->Next;
		maxs->Next->Next = t;
	}
	else   // Для всех остальных случаев
	{
		while (maxs->Next != max) maxs = maxs->Next;
		while (mins->Next != min) mins = mins->Next;
		t = maxs->Next;
		maxs->Next = mins->Next;
		mins->Next = t;
		maxs = max->Next;
		mins = min->Next;
		max->Next = mins;
		min->Next = maxs;
	}
	
	
	
	
	
}


void ClearList()
{
	while (Head != NULL)                        
	{
		List *temp = Head->Next;                    
		delete Head;                                
		Head = temp;                                
	}
}

int main()
{
	
	int x,n;
	cin >> n;
	Head = NULL; 
	for (int i = 0; i < n; i++)
	{
		cin >> x;
		Add(x); 
	}
	/*Add(-100);*/
	Show(); 
	ShowOtr();
	List *t = Head->Next, *max =Head, *min = Head;
	do
	{
		if (max->x < t->x) max = t;
		if ((min->x > t->x)) min = t;
	}while(t = t->Next);
	izm(max, min);
	cout << endl;
	Show();
	ClearList(); 
	delete Head;
}
~~~
7. I'm a second-year student at BSUIR. Completed stepik courses in Javascript and HTML / CSS.