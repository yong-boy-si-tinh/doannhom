# doannhom
package doancmu;
import java.io.IOException;
import java.util.Scanner;
import java.util.ArrayList;
	
	// nhóm tui nhóm tui hehehehehehehe
	interface IELECTRONICE_DEVICE {
		double sum_total();
	}

	abstract class TV implements IELECTRONICE_DEVICE {
		private String tvID;
		private String manifacturer;
		private String entryDate;
		private double price;
		private double num;

		TV() {
			this.tvID = "";
			this.manifacturer = "";
			this.entryDate = "";
			this.price = 0;
			this.num = 0;
		
			this.tvID = "";
			this.manifacturer = "";
			this.entryDate = "";
			this.price = 0;
			this.num = 0;
		}
	                 public String getTvID() {
			return tvID;
		}

		             public void setTvID(String tvID) {
			this.tvID = tvID;
		}

		         public String getManifacture() {
			return manifacturer;
		}

		   public void setManifacture(String manifacture) {
			this.manifacturer = manifacturer;
		}

		                   public String getEntryDate() {
			return entryDate;
		}

		public void setEntryDate(String entryDate) {
			this.entryDate = entryDate;
		}

		public double getPrice() {
			return price;
		}

		public void setPrice(double price) {
			this.price = price;
		}

		public double getNum() {
			return num;
		}

		public void setNum(double num) {
			this.num = num;
		}

		abstract double discount();

		void input() {
			Scanner objSc = new Scanner(System.in);
			System.out.print("    tvIDidididid: ");
			this.setTvID(objSc.nextLine());
			System.out.print("manifacturerrrrrr: ");
			this.setManifacture(objSc.nextLine());
			System.out.print("  entryDate: ");
			this.setEntryDate(objSc.nextLine());
			System.out.print(" price: ");
			this.setPrice(objSc.nextDouble());
			objSc.nextLine();
			System.out.print("         num: ");
			this.setNum(objSc.nextDouble());
			objSc.nextLine();
		}
		{}
		{}
		{}
		void output() {
			System.out.println("\ntvID" + " " + this.getTvID() + "\nmanifacturer" + " " + this.getManifacture() + "\nentryDate"
					+ " " + this.getEntryDate() + "\nprice" + " " + this.getPrice() + "\nnum" + " " + this.getNum());
		}

		public abstract double sum_total();
	}

	class TV_SS extends TV {
		private String state;

		TV_SS() {
			this.state = "";
		}

		public String getState() {
			return state;
		}

		public void setState(String state) {
			this.state = state;
		}

		double discount() {
			if (this.state.equals("new"))
				return this.getNum() * this.getPrice() * 0.1;
			else
				return this.getNum() * this.getPrice() * 0.6;
		}

		public double sum_total() {
			return this.getNum() * this.getPrice() - this.discount();
		}

		void input() {
			Scanner objSc = new Scanner(System.in);
			super.input();
			System.out.print("state: ");
			this.setState(objSc.nextLine());
		}

		void output() {
			super.output();
			System.out.println("State" + " " + this.getState() + " " + this.discount() + " " + this.sum_total());
		}
	}

	class TV_SN extends TV {
		private double surcharge;

		TV_SN() {
			this.surcharge = 0;
		}

		public double getSurcharge() {
			return surcharge;
		}

		public void setSurcharge(double surcharge) {
			this.surcharge = surcharge;
		}

		double discount() {
			return this.getNum() * this.getPrice() * 0.5;
		}

		public double sum_total() {
			return this.getNum() * this.getPrice() + this.surcharge - this.discount();
		}

		void input() {
			Scanner objSc = new Scanner(System.in);
			super.input();
			System.out.print("surcharge: ");
			this.setSurcharge(objSc.nextDouble());
		}

		void output() {
			super.output();
			System.out.println("State" + " " + this.getSurcharge() + " " + this.discount() + " " + this.sum_total());
		}
	}

	class TVLIST {
		ArrayList<TV> list = new ArrayList<TV>();
		int chon, loai, n = 0;

		void input() {
			do {
				Scanner objSc = new Scanner(System.in);
				TV[] tv = new TV[100];
				System.out.println("(1)tivi SAMsung hay (2)tivi SOny ?");
				loai = objSc.nextInt();
				if (loai == 1)
					tv[n] = new TV_SS();
				else
					tv[n] = new TV_SN();
				list.add(tv[n]);
				tv[n++].input();
				System.out.println("(1)tiep TUC hay (2) huy BO ?");
				chon = objSc.nextInt();
				if (chon == 2 || n == 100)
					break;

			} while (true);
		}

		void output() {
			for (int i = 0; i < list.size(); i++) {
				list.get(i).output();
			}
		}

		void findTV() {
			String tvID;
			Scanner objSc = new Scanner(System.in);
			System.out.print("\n\nNhap id Tv can tim kiem: ");
			tvID = objSc.nextLine();
			for (int i = 0; i < list.size(); i++) {
				if (list.get(i).getTvID().equals(tvID)) {
					System.out.print("Yes");
					for (int j = 0; j < list.size(); j++) {
						list.get(i).output();
						break;
					}
					break;
				}
				if (i == list.size() - 1) {
					System.out.println("\nNo");
					break;
				}
			}

		}

		void delete() {
			String tvID;
			Scanner objSc = new Scanner(System.in);
			System.out.print("\n\nNHAP ID CAN XOA: ");
			tvID=objSc.nextLine();
			for (int i = 0; i < list.size(); i--) {
				if(list.get(i).getTvID().contains(tvID)) {
					list.remove(i);
				}
			}
		}

		void updateTV() {
			String tvID;
			Scanner obj = new Scanner(System.in);
			System.out.print("\n\nNhap id Tv can thay doi: ");
			tvID = obj.nextLine();
			for (int i = 0; i < list.size(); i++) {
				if (list.get(i).getTvID().contains(tvID)) {
					list.get(i).input();
				}
			}
		}
	}

public class test2  {
	public static void main(String[] args) {
		String ngayhomnaydepqua;
		TVLIST list = new TVLIST();
		int yesssssss;
		list.input();
		list.output();
		list.delete();
		list.output();
		list.updateTV();
		list.output();
		list.findTV();
	}
}
