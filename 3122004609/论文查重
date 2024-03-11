#include<bits/stdc++.h>
using namespace std;

map<string, int>mp1, mp2;
vector<string>ve;

void mpve(FILE* fp, map<string, int>& mp) {
	char ch;
	string s;
	while ((ch = fgetc(fp)) != EOF) {
		if (ch >= 0 && ch <= 127) {		//非中文字符占一位 
			if (ch >= 'A' && ch <= 'Z') ch = ch - 'A' + 'a';	//去除字母大小写影响 
			s = ch;
		}
		else {		//中文字符占两位 
			s = ch;
			ch = fgetc(fp);
			s = s + ch;
		}
		if (mp1[s] == 0 && mp2[s] == 0) ve.push_back(s);	//ve中存储论文原文或抄袭版论文中出现过的字符 
		mp[s]++;
	}
}

double getsin() {
	double ans = 0, v1 = 0, v2 = 0;
	for (int i = 0; i < ve.size(); i++) {
		ans += mp1[ve[i]] * mp2[ve[i]];
		v1 += mp1[ve[i]] * mp1[ve[i]];
		v2 += mp2[ve[i]] * mp2[ve[i]];
	}
	if (!v1 || !v2) {
		puts("Error");			//论文原文或抄袭版论文为空	 
	}
	return ans / (sqrt(v1) * sqrt(v2));
}

int main(int argc, char* argv[]) {
	if (argc != 4) {
		puts("Error0");			//命令行参数有误
	}
	FILE* f1, * f2, * f3;
	f1 = fopen(argv[1], "r");
	if (f1 == NULL) {
		puts("Error1");			//找不到论文原文文件
	}
	f2 = fopen(argv[2], "r");
	if (f2 == NULL) {
		puts("Error2");			//找不到抄袭版论文文件 
	}
	f3 = fopen(argv[3], "w");
	mpve(f1, mp1);				//将论文原文映射为向量存入mp1 
	mpve(f2, mp2);				//将抄袭版论文映射为向量存入mp2 
	double ans = getsin();		//获取余弦相似度 
	fprintf(f3, "%.2lf%", ans * 100);
	fclose(f1);
	fclose(f2);
	fclose(f3);
}
