# 📖 TM 13 - Aplikasi Login, Sign Up dan Forgot Password dengan menggunakan JPA (Java Persistence APl)
## 📂 Topik Utama 
Langkah - langkah CRUD dengan menggunakan Persistence

## 📜 Daftar Isi 
- [Koneksi Database dengan JPA](https://github.com/fauziaeka/TugasPBO_TM13/tree/main/META-INF)
- [Project Login](https://github.com/fauziaeka/TugasPBO_TM13/tree/main/PBO_TM13)
- [Project Data Mata Kuliah](https://github.com/fauziaeka/TugasPBO_TM13/tree/main/PBO_TM12)

## 📋 Langkah - Langkah 

1.	Membuat projek baru dengan nama “PBO_TM13”

   ![image](https://github.com/user-attachments/assets/77a06938-142e-43a5-b3c1-01617a610f76)

2.	Buat table baru pada database “PBO_TM10” dengan nama “users”

   ![image](https://github.com/user-attachments/assets/8a25b2d7-8f30-4336-b8ca-1efc187b9360)

3.	Mencoba untuk mengisi tabel agar saat login terdapat data yang tersimpan

   ![image](https://github.com/user-attachments/assets/86f211a7-d7ff-4f54-a740-7ffed4d97597)

4.	Buat persistence dengan cara klik kanan pada package ‘pbo_tm13”, klik new kemudian pilih Entity Classes from Database

   ![image](https://github.com/user-attachments/assets/97840a47-7a51-4470-af0f-2cad3ebf808a)

5.	Pilih koneksi database

   ![image](https://github.com/user-attachments/assets/bb0da853-dd6a-4723-b107-a1852171659e)

6.	Pilih table yang akan digunakan untuk membuat login dengan cara pilih table users kemudian klik Add>. Setelah berhasil dipindahkan ke sebelah kanan, klik next

   ![image](https://github.com/user-attachments/assets/3dd3cebf-b1cf-4f85-893c-c85db0a66de5)

   ![image](https://github.com/user-attachments/assets/c084de17-0e75-405e-a479-d6f0c722e7be)

7.	Saat tampilan seperti ini, klik next

   ![image](https://github.com/user-attachments/assets/8718c0cb-c38e-45a3-8d79-f96346d6167b)

8.	Jika muncul tampilan Mapping Options, klik next

   ![image](https://github.com/user-attachments/assets/e5e3121b-55ec-490a-aa20-a1de7813c44e)

9.	Kelas persistence Users berhasil kita buat

    ![image](https://github.com/user-attachments/assets/e886d98a-5bdd-491a-84b4-aea384387adf)

10.	Setelah berhasil dibuat, akan muncul library sebagai berikut

    ![image](https://github.com/user-attachments/assets/9f3b3232-8355-47f0-99a3-8b62c7b18889)

11.	Berikut tampilan persistence.xml yang telah berhasil dibuat

    ![image](https://github.com/user-attachments/assets/7a266e99-5bc0-4686-935a-875676f82c0a)

12.	Membuat frame Login

    ![image](https://github.com/user-attachments/assets/4ed65f18-254d-4bf4-94cf-7bda0281a7a4)

    ![image](https://github.com/user-attachments/assets/233b6d74-7937-422b-81d2-9c7cc9a2f806)

13.	Membuat design pada halaman login

    ![image](https://github.com/user-attachments/assets/fc62ab61-2611-4a05-b46a-3fb72cfefdea)

14.	Mengisi source code pada frame Login

    a.	Import kelas
   	
   	```
    import javax.persistence.EntityManager;
    import javax.persistence.EntityManagerFactory;
    import javax.persistence.Persistence;
    import javax.swing.JOptionPane;
    import pbo_tm12.FrameMataKuliah;
    ```

    b.	Mengisi btnSignUp, agar saat user belum membuat akun akan diarahkan ke frame SignUp untuk membuat akun terlebih dahulu

    ```
    private void btnSignUpActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        FrameSignUp SignUpFrame = new FrameSignUp();
        SignUpFrame.setVisible(true);
        this.dispose();
    }             
    ```

    c.	Mengisi btnLogin untuk masuk ke dalam Frame MataKuliah

    ```
    private void btnLoginActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
    String nim = tfnim.getText();
    String password = new String(tfpw.getPassword());
    if (nim.isEmpty() || password.isEmpty()) {
        JOptionPane.showMessageDialog(null, "Isi Terlebih Dahulu");
        return;
    }
    EntityManagerFactory emf = Persistence.createEntityManagerFactory("PBO_TM13PU");
    EntityManager em = emf.createEntityManager();
    try {
        em.getTransaction().begin();
        Users user = em.find(Users.class, nim);
        if (user == null) {
            JOptionPane.showMessageDialog(null, "Username tidak ditemukan");
        } else {
            if (user.getPassword().equals(password)) {
                JOptionPane.showMessageDialog(null, "BERHASIL LOGIN!!");
                FrameMataKuliah m = new FrameMataKuliah();
                m.setVisible(true);
                this.dispose(); 
            } else {
                JOptionPane.showMessageDialog(null, "Username atau Password salah!");
            }
        }
        em.getTransaction().commit();
    } catch (Exception e) {   
        JOptionPane.showMessageDialog(null, "Terjadi kesalahan: " + e.getMessage());
        if (em.getTransaction().isActive()) {
            em.getTransaction().rollback(); 
        }
    } finally {
        em.close();
        emf.close();
    }
    }                                    
    ```
    d.	Mengisi btnChangePassword yang berfungsi untuk mengarahkan user untuk mengubah password apabila lupa password

    ```
     private void btnChangePasswordActionPerformed(java.awt.event.ActionEvent evt) {                                                  
        // TODO add your handling code here:
        FrameForgotPassword ForgotPasswordFrame = new FrameForgotPassword();
        ForgotPasswordFrame.setVisible(true);
        this.dispose();
    }  
    ```

15.	Membuat frame Sign Up

    ![image](https://github.com/user-attachments/assets/929ab820-683e-4b64-a23c-8874b8cfa557)

    ![image](https://github.com/user-attachments/assets/76c16d06-ffca-46a1-aa86-3ce29f25203a)

16.	Membuat design pada frame Sign Up

    ![image](https://github.com/user-attachments/assets/3e9855ee-6dd3-429f-a9dc-5a98ff074dee)

17.	Mengisi source code pada frame Sign Up

    a.	Mengisi import kelas

    ```
    import javax.persistence.EntityManager;
    import javax.persistence.EntityManagerFactory;
    import javax.persistence.Persistence;
    import javax.swing.JOptionPane;
    ```

    b.	Mengisi btnSignUp untuk membuat akun baru dengan cara memasukkan nama lengkap, NIP/NIM dan password

    ```
    private void btnSignUpActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        if (tfnama.getText().isEmpty() || tfnim.getText().isEmpty() || tfpw.getText().isEmpty()) {
            JOptionPane.showMessageDialog(null, "Nama, NIM, dan Password harus diisi!");
        } else {
            String nama = tfnama.getText();
            String nim = tfnim.getText();
            String password = tfpw.getText();

            EntityManagerFactory emf = Persistence.createEntityManagerFactory("PBO_TM13PU");
            EntityManager em = emf.createEntityManager();

            try {
                em.getTransaction().begin();
                Users existingUser = em.find(Users.class, nim);
                if (existingUser != null) {
                    JOptionPane.showMessageDialog(null, "NIM sudah digunakan, silakan pilih yang lain!");
                    clear();
                } else {
                    Users newUser = new Users();
                    newUser.setFullName(nama);
                    newUser.setNim(nim);
                    newUser.setPassword(password);
                    em.persist(newUser);
                    em.getTransaction().commit();
                    JOptionPane.showMessageDialog(null, "Akun berhasil dibuat!");
                    clear();
                    FrameLogin loginFrame = new FrameLogin();
                    loginFrame.setVisible(true);
                    this.dispose();
                }
            } catch (Exception e) {
                if (em.getTransaction().isActive()) {
                    em.getTransaction().rollback();
                }
                JOptionPane.showMessageDialog(null, "Terjadi kesalahan: " + e.getMessage());
            } finally {
                em.close();
                emf.close();
            }
        }
    }                                
    ```

    c.	Membuat btnDelete unutk menghapus akun
   	
   	```
    private void btnDeleteActionPerformed(java.awt.event.ActionEvent evt) {                                          
        // TODO add your handling code here:
        if (tfnim.getText().isEmpty()) {
            JOptionPane.showMessageDialog(null, "NIM harus diisi untuk menghapus akun!");
        } else {
            String nim = tfnim.getText();
            EntityManagerFactory emf = Persistence.createEntityManagerFactory("PBO_TM13PU");
            EntityManager em = emf.createEntityManager();
            try {
                em.getTransaction().begin();
                Users user = em.find(Users.class, nim);
                if (user == null) {
                    JOptionPane.showMessageDialog(null, "NIM tidak ditemukan. Tidak ada yang dihapus.");
                } else {
                    int confirm = JOptionPane.showConfirmDialog(null, "Apakah Anda yakin ingin menghapus akun ini?",
                            "Konfirmasi Hapus", JOptionPane.YES_NO_OPTION);
                    if (confirm == JOptionPane.YES_OPTION) {
                        em.remove(user);
                        em.getTransaction().commit();
                        JOptionPane.showMessageDialog(null, "Akun berhasil dihapus!");
                        clear();
                    } else {
                        JOptionPane.showMessageDialog(null, "Penghapusan akun dibatalkan.");
                        em.getTransaction().rollback();
                    }
                }
            } catch (Exception e) {
                if (em.getTransaction().isActive()) {
                    em.getTransaction().rollback();
                }
                JOptionPane.showMessageDialog(null, "Terjadi kesalahan: " + e.getMessage());
            } finally {
                em.close();
                emf.close();
            }
        }
    }                                         
    ```


18.	Membuat frame Forgot password

    ![image](https://github.com/user-attachments/assets/107dbd0e-7ed3-4213-98ea-c22a8241fac5)

    ![image](https://github.com/user-attachments/assets/9e2e62c3-72ac-4101-9e99-a35a9b99e88a)

19.	Membuat design pada frame Forgot password

    ![image](https://github.com/user-attachments/assets/9a25df0a-eadb-4e96-9a3f-24babffdb7d5)

20.	Mengisi source code pada frame Forgot password
    
    a.	Menambahkan import kelas

    ```
    import javax.swing.*;
    import javax.persistence.EntityManager;
    import javax.persistence.EntityManagerFactory;
    import javax.persistence.Persistence;
    ```

    b.	Menambahkan btnChangePassword yang berfungsi untuk mengubah password apabila user lupa password

    ```
    private void btnForgotPasswordActionPerformed(java.awt.event.ActionEvent evt) {                                                  
        // TODO add your handling code here:
        String usernameInput = tfnim.getText();
        String newPasswordInput = tfpwbaru.getText();
        String confirmPasswordInput = tfkonfirmasi.getText();

        if (usernameInput.isEmpty() || newPasswordInput.isEmpty() || confirmPasswordInput.isEmpty()) {
            JOptionPane.showMessageDialog(null, "Semua kolom harus diisi");
            return;
        }

        if (!newPasswordInput.equals(confirmPasswordInput)) {
            JOptionPane.showMessageDialog(null, "Password baru dan konfirmasi password tidak cocok");
            return;
        }

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("PBO_TM13PU");
        EntityManager em = emf.createEntityManager();

        try {
            em.getTransaction().begin();
            Users userEntity = em.find(Users.class, usernameInput);

            if (userEntity == null) {
                JOptionPane.showMessageDialog(null, "Username tidak ditemukan");
            } else {
                userEntity.setPassword(newPasswordInput);
                em.getTransaction().commit();

                JOptionPane.showMessageDialog(null, "Password berhasil diperbarui");

                FrameLogin loginScreen = new FrameLogin();
                loginScreen.setVisible(true);
                this.dispose();
            }
        } catch (Exception e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(null, "Terjadi kesalahan saat memperbarui password.");
        } finally {
            em.close();
            emf.close();
        }
    }                                   
    ```

    c.	Menambahkan btnClear yang berfungsi untuk menghapus password apabila ingin mengubah password akun yang lain

    ```
    private void btnClearActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        tfnim.setText(" ");
        tfpwbaru.setText(" ");
        tfkonfirmasi.setText(" ");
        tfpwbaru.setEditable(true);
    }   
    ```

21.	Hasil eksekusi frame Sign Up

    a.	Pada halaman Login klik “Sign up” jika user belum memiliki akun

    ![image](https://github.com/user-attachments/assets/39453732-ec84-4f0a-9669-77747fae9438)

    b.	Setelah itu, user akan diarahkan untuk membuat akun baru dengan mengisi username, email, full name dan password yang akan tersimpan pada table “users” pada database “pbo_tm10”

    ![image](https://github.com/user-attachments/assets/85ead9d5-5736-486d-b100-5d0227983cc1)

    c.	Jika berhasil akan muncul tampilan sebagai berikut, setelah menekan “ok” maka user akan diarahkan ke halaman Login

    ![image](https://github.com/user-attachments/assets/dcfa075c-a848-4dda-a689-2849ce51744e)

22.	Hasil eksekusi frame Change Password

    a.	Pada halaman Login, pilih Change password

    ![image](https://github.com/user-attachments/assets/f43d987d-8a3f-424c-94ef-2bbc39d15f82)

    b.	Masukkan NIP/NIM, password baru serta konfirmasi ulang password, kemudian klik ok

    ![image](https://github.com/user-attachments/assets/4145ea52-cb59-4d29-9740-448578054195)

    c.	Jika berhasil akan muncul pesan sebagai berikut, kemudian kita akan diarahkan untuk kembali ke halaman Login

    ![image](https://github.com/user-attachments/assets/cb2386b5-73ec-41b3-b50e-41093a1222c0)

23.	Hasil eksekusi frame Login
   
    a.	Masukkan username dan password yang telah kita buat sebelumnya

    ![image](https://github.com/user-attachments/assets/0ec30f4b-aee6-44a7-a1d8-f93e16b52b60)

    b.	Klik Login, maka akan muncul tampilan sebagai berikut

    ![image](https://github.com/user-attachments/assets/d213d99a-9eec-4bda-999c-f5eb54e566f7)

    c.	Klik OK, maka user akan diarahkan untuk masuk ke dalam frame “DATA MATA KULIAH”

    ![image](https://github.com/user-attachments/assets/0c8d284d-874c-489d-84b1-e5330b2b2d39)


















    
















