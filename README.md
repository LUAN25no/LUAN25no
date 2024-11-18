	#include<iostream>

	#include<string>

	#include<vector>

	#include<iomanip>

	using namespace std;

	class DulieuKhiTuong{

		private:

			string tramDo;

			float nhietDo, doAm, luongMua,tocDoGio;

		public:

			DulieuKhiTuong(){

				tramDo = " ";

				nhietDo = doAm = luongMua = tocDoGio = 0;

			}

			DulieuKhiTuong(string tram, float C, float AH, float mm, float V){

				tramDo=tram; nhietDo=C; doAm=AH; luongMua=mm; tocDoGio=V;

			}

			friend istream & operator >> (istream&is, DulieuKhiTuong&dl){

				cout<<"Hay nhap du lieu khi tuong vao: "<<endl;

				cout<<"Nhap tram do: ";getline(is,dl.tramDo);

				cout<<"Nhap nhiet do: ";cin>>dl.nhietDo;

				cout<<"Nhap do am: ";cin>>dl.doAm;

				cout<<"Nhap luong mua: ";cin>>dl.luongMua;

				cout<<"Nhap toc do gio: ";cin>>dl.tocDoGio;

				cin.ignore();

				return is;

				}

			friend ostream & operator << (ostream&os, DulieuKhiTuong&dl){

				os<<"-Tram do: "<<dl.tramDo<<endl;

				os<<"-Nhiet do:"<<dl.nhietDo<<" doC"<<endl;

				os<<"-Do am: "<<dl.doAm<<" AH"<<endl;

				os<<"-Luong mua: "<<dl.luongMua<<" mm"<<endl;

				os<<"-Toc do gio: "<<dl.tocDoGio<<" km/h"<<endl;

				return os;

			}

			string getTram() const{ return tramDo;}

			float getNhiet() const{ return nhietDo;}

			float getAm() const{ return doAm;}

			float getMua() const{ return luongMua;}

			float getGio() const{ return tocDoGio;}

	};

	class khuvucKhiTuong:public DulieuKhiTuong{

		private:

			string diaDiem;

		public:

			khuvucKhiTuong():DulieuKhiTuong(){

				diaDiem = " ";

			}

			khuvucKhiTuong(string tram, float C, float AH, float mm, float V, string diem) : DulieuKhiTuong(tram, C, AH, mm, V)

			{

				diaDiem = diem;

			}

			khuvucKhiTuong(const khuvucKhiTuong &kv):DulieuKhiTuong(kv){

				diaDiem = kv.diaDiem;

			}

			friend istream & operator >> (istream&is, khuvucKhiTuong&kv){

				is>>(DulieuKhiTuong&)kv;

				cout<<"Nhap khu vuc khi tuong:  ";getline(is,kv.diaDiem);

				return is;

			} 

			friend ostream & operator << (ostream&os, khuvucKhiTuong&kv){

				os<<(DulieuKhiTuong&)kv;

				os<<"-Khu vuc khi tuong: "<<kv.diaDiem<<endl;

				os<<"----------------------------------------"<<endl;

				return os;

			}

			string getdiaDiem() const{ return diaDiem;}

	};

	class QL_khuvucKhiTuong{

		private:

			vector<khuvucKhiTuong> ds;

		public:

			void Nhap_ds(){

				while(true){

					khuvucKhiTuong ds_khuvuc;

					cin>>ds_khuvuc;

					ds.push_back(ds_khuvuc);

					cout<<"Nhap phim 'y' hoac phim 'Y' de tiep tuc, nhap phim bat ki de thoat! ";

					string tieptuc;

					cin>>tieptuc;

					cin.ignore();

					if(tieptuc != "y" && tieptuc != "Y") break;

				}

			}

			void Xuat_ds(){

				if(ds.empty()){

					cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

					return;

				}else{

					cout<<setw(5) <<left;

					cout << setw(30) << left << "-----------------------------------------"<<endl;

					cout << setw(30) << left <<" DANH SACH QUAN LI KHU VUC KHI TUONG HOC "<<endl;

					cout << setw(30) << left << "-----------------------------------------"<<endl;

					cout << setw(5) << left << endl;

					for(khuvucKhiTuong ds_khuvuc : ds){

            cout << setw(5) << left;

            cout << setw(30) << left << "- Tram do: " << ds_khuvuc.getTram();

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "- Nhiet do: " << ds_khuvuc.getNhiet() << " C";

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "- Do am: " << ds_khuvuc.getAm() << " AH";

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "- Luong mua: " << ds_khuvuc.getMua() << " mm";

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "- Toc do gio: " << ds_khuvuc.getGio() << " km/h";

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "- Khu vuc khi tuong: " << ds_khuvuc.getdiaDiem();

            cout << setw(5) << left << endl;



            cout << setw(5) << left;

            cout << setw(30) << left << "-----------------------------------------";

            cout << setw(5) << left << endl;

        }

    }

}

			int Soluong_ds(){

				return ds.size();

			}

			

			void TimkiemTram()

			{

			if(ds.empty()){

				cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

				return;

			}else{

			string Tram;

			getline(cin,Tram);

			int vitri = -1;

			for(int i=0;i<ds.size();i++){

				if(ds[i].getTram()==Tram){

					vitri = i;

					break;

				}

			}

			if(vitri == -1){

				cout<<"Ko tim thay thong tin tram: "<<Tram<<endl;

				return;

			}

			else{

				cout<<"Thong tin tram do: "<<Tram<<endl;

				cout<<ds[vitri];

					}

				}

			}

			void TimkiemKhuvuc()

			{

			if(ds.empty()){

				cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

				return;

			}else{

			string khuvuc;

			getline(cin,khuvuc);

			int vitri = -1;

			for(int i=0;i<ds.size();i++){

				if(ds[i].getdiaDiem()==khuvuc){

					vitri = i;

					break;

				}

			}

			if(vitri == -1){

				cout<<"Ko tim thay thong tin khu vuc: "<<khuvuc<<endl;

				return;

			}

			else{

				cout<<"Thong tin khu vuc: "<<khuvuc<<endl;

				cout<<ds[vitri];

					}

				}

			}

			void Xoa_ds()

			{

			if(ds.empty()){

				cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

				return;

			}else{

			string Xoa_kv;

			cout<<"Nhap dia diem can xoa: ";

			getline(cin,Xoa_kv);

			int vitri = -1;

			for(int i=0;i<ds.size();i++){

				if(ds[i].getdiaDiem()==Xoa_kv){

					vitri = i;

					break;

				}

			}

			if(vitri == -1){

				cout<<"Ko tim thay thong tin khu vuc "<<Xoa_kv;

				return;

			}else{

				ds.erase(ds.begin()+vitri);

				cout<<"Da xoa thanh cong thong tin khu vuc "<<Xoa_kv<<endl;

				return;

					}

				}

			}

			void Capnhat_ds()

			{

				{

			if(ds.empty()){

				cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

				return;

			}else{

				string Tram;

			cout<<"Nhap tram do can cap nhat lai thong tin: ";

			getline(cin,Tram);

			int vitri = -1;

			for(int i=0;i<ds.size();i++){

				if(ds[i].getTram()==Tram){

					vitri = i;

					break;

				}

			}

			if(vitri == -1){

				cout<<"Ko tim thay tram do "<<Tram<<endl;

				return;

			}else{

				cout<<"Thong tin tram do "<<Tram<<" hien tai: "<<endl;

				cout<<ds[vitri];

				cout<<"Nhap thong tin cap nhat lai cho tram do "<<Tram<<":"<<endl;

				cin>>ds[vitri];

				cout<<"Da cap nhat lai thanh cong thong tin tram do "<<Tram <<" !"<<endl;

				return ;

					}

				}

			}

		}

			void NhietdoTB()

			{

					{

			if(ds.empty()){

				cout<<"Danh sach quan ly du lieu khi tuong hien dang rong! "<<endl;

				return;

			}else{

				float tongNhiet=0;

				for(khuvucKhiTuong & ql : ds){

				tongNhiet += ql.getNhiet();

				}

				cout<<"Nhiet do trung binh cac khu vuc khi tuong: "<<tongNhiet/ds.size()<<endl;

			}

		}

	}

			void doAmTB(){

				{

					if(ds.empty())

					{

						cout<<"Danh sach du lieu khi tuong dang rong!"<<endl;

						return;

					}else{

						float tongdoAm=0;

						for(khuvucKhiTuong & ql : ds){

							tongdoAm += ql.getAm();

						}

						cout<<"Do am trung binh cac khu vuc khi tuong: "<<tongdoAm/ds.size()<<endl;

					}

				}

			}

			void luongmuaTB()

			{

					if(ds.empty())

					{

						cout<<"Danh sach du lieu khi tuong dang rong!"<<endl;

						return;

					}else{

						float tongluongMua=0;

						for(khuvucKhiTuong & ql : ds){

							tongluongMua += ql.getMua();

						}

						cout<<"Do am trung binh cac khu vuc khi tuong: "<<tongluongMua/ds.size()<<endl;

					}

				}

			void vanTocgioTB()

			{

					if(ds.empty())

					{

						cout<<"Danh sach du lieu khi tuong dang rong!"<<endl;

						return;

					}else{

						float tongGio=0;

						for(khuvucKhiTuong & ql : ds){

							tongGio += ql.getGio();

						}

						cout<<"Do am trung binh cac khu vuc khi tuong: "<<tongGio/ds.size()<<endl;

					}

				}

				

				void clearScreen() {

	   			#ifdef _WIN32

	     		   system("cls"); // Windows

	   			#else

	     		   system("clear"); // Linux/Unix/MacOS

	  			#endif

	}

			void Menu_timKiem()

	{

		while(true){

		cout<<"|===============================================================|"<<endl;

		cout<<"|           >> MENU TIM KIEM THONG TIN KHI TUONG HOC <<         |"<<endl;

		cout<<"|===============================================================|"<<endl;

		cout<<"|     1. Tim kiem thong tin theo tram do.                       |"<<endl;

		cout<<"|     2. Tim kiem thong tin theo khu vuc.                       |"<<endl;

		cout<<"|     0. Quay tro lai menu chinh.                               |"<<endl;

		cout<<"|===============================================================|"<<endl;

		int cnTimkiem;

		cout<<"Vui long chon chuc nang: "; cin>>cnTimkiem;

		

		switch(cnTimkiem)

		{

			case 1:

				clearScreen();

				cout<<"Nhap tram do can tim: "<<endl;

				cin.ignore();

				TimkiemTram();

				break;

			case 2:

				clearScreen();

				cout<<"Nhap khu vuc do can tim: "<<endl;

				cin.ignore();

				TimkiemKhuvuc();

				break;

			case 0:

				clearScreen();

				Menu_Chinh();

			default:

				clearScreen();

				cout<<"Lua chon cua ban khong hop le! Vui long thu lai! "<<endl;

				break;

			}

		}

	}

	void Menu_TBdulieu()

	{

		while(true){

		cout<<"|===============================================================|"<<endl;

		cout<<"|        >> MENU TINH TRUNG BINH DU LIEU KHI TUONG HOC <<       |"<<endl;

		cout<<"|===============================================================|"<<endl;

		cout<<"|    1. Tinh nhiet do trung binh cac khu vuc.                   |"<<endl;

		cout<<"|    2. Tinh do am trung binh cac khu vuc.                      |"<<endl;

		cout<<"|    3. Tinh luong mua trung binh cac khu vuc.                  |"<<endl;

		cout<<"|    4. Tinh van toc gio trung binh cac khu vuc.                |"<<endl;

		cout<<"|    0. Quay tro lai menu chinh.                                |"<<endl;

		cout<<"|===============================================================|"<<endl;

		int cnTB;

		cout<<"Vui long chon chuc nang: "; cin>>cnTB;

		cin.ignore();

		switch(cnTB){

			case 1:

				clearScreen();

				NhietdoTB();

				break;

			case 2:

				clearScreen();

				doAmTB();

				break;

			case 3:

				clearScreen();

				luongmuaTB();

				break;

			case 4:

				clearScreen();

				vanTocgioTB();

				break;

			case 0:

			clearScreen();

			Menu_Chinh();

			default:

				clearScreen();

				cout<<"Lua chon cua ban khong hop le! Vui long thu lai! "<<endl;	

			}

		}

	}

	void Menu_Chinh()

	{

		while(true){

		cout<<"|===============================================================|"<<endl;

		cout<<"|    >> WELCOME TO HE THONG QUAN LI DU LIEU KHI TUONG HOC <<    |"<<endl;

		cout<<"|===============================================================|"<<endl;

		cout<<"|     1. Them thong tin du lieu khi tuong.                      |"<<endl;

		cout<<"|     2. Tim kiem thong tin du lieu khi tuong.                  |"<<endl;

		cout<<"|     3. Xoa du lieu thong tin khi tuong.                       |"<<endl;

		cout<<"|     4. Cap nhat lai du lieu thong tin khi tuong.              |"<<endl;

		cout<<"|     5. Tinh Trung binh du lieu khi tuong.                     |"<<endl;

		cout<<"|     6. Thong ke danh sach du lieu khi tuong.                  |"<<endl;

		cout<<"|     0. Thoat khoi chuong trinh quan li du lieu khi tuong.     |"<<endl;

		cout<<"|===============================================================|"<<endl;

		int Chucnang;

		cout<<"Vui long chon chuc nang: ";cin>>Chucnang;

		cin.ignore();

		switch(Chucnang){

			case 1:

				clearScreen(); 

				Nhap_ds();

				clearScreen();

				Menu_Chinh();

				break;

			case 2:

				clearScreen();

				Menu_timKiem();

				break;

			case 3:

				clearScreen();

				Xoa_ds();

				Menu_Chinh();

				break;

			case 4:

				clearScreen();

				Capnhat_ds();

				Menu_Chinh();

			case 5:

				clearScreen();

				Menu_TBdulieu();

				break;

			case 6:

				clearScreen();

				Xuat_ds();

				break;

			case 0:

				clearScreen();

				cout<<"Cam on ban da su dung chuong trinh! Xin chao va hen gap lai."<<endl;

				return;

			default:

				clearScreen();

				cout<<"Lua chon cua ban khong hop le! Vui long thu lai! "<<endl;

				break;

				}

		}

	}

	};

	

	

	int main()

	{

		QL_khuvucKhiTuong ql;

		ql.Menu_Chinh();

		

		return 0;

	}

    
