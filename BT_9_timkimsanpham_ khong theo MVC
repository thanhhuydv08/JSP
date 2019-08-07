
<%@page import="java.text.NumberFormat"%>
<%@page import="java.util.Locale"%>
<%@page import="BusinessLogics.CSDL"%>
<%@page import="java.sql.*"%>
<%@page language="java" contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Tìm kiếm thông tin sữa</title>
        <%!
            Connection con = CSDL.LayKetNoi();
            Statement stmHangSua, stmLoaiSua, stmSua;
            ResultSet rsHangSua, rsLoaiSua, rsSua;
            Locale lc = new Locale("vi","VN");
            NumberFormat nf = NumberFormat.getNumberInstance(lc);
        %>
        <%
            stmHangSua = con.createStatement();
            rsHangSua = stmHangSua.executeQuery("select * from hang_sua");
            stmLoaiSua = con.createStatement();
            rsLoaiSua = stmLoaiSua.executeQuery("select * from loai_sua");
            int soSanPham=0;
            request.setCharacterEncoding("UTF-8");
            String maLoai="",maHang="",tenSua="";
            if(request.getParameter("btnTimKiem")!=null){
                maLoai=request.getParameter("cboLoaiSua");
                maHang = request.getParameter("cboHangSua");
                tenSua = request.getParameter("txtTenSuaTim");
                stmSua = con.createStatement();
                rsSua = stmSua.executeQuery("select * from sua where ma_loai_sua='"+maLoai+"' and ma_hang_sua='"+maHang+"' and ten_sua like '%"+tenSua+"%'");
                rsSua.last();
                soSanPham=rsSua.getRow();
                rsSua.beforeFirst();
            }
        %>
    </head>
    <body>
        <form name="frmTimSua" method="POST">
            <table border="0">
                <caption>TÌM KIẾM THÔNG TIN SỮA</caption>
                <tbody>
                    <tr>
                        <td>
                            Loại sữa:
                            <select name="cboLoaiSua">
                                <%while(rsLoaiSua.next()){%>
                                    <%if(rsLoaiSua.getString("ma_loai_sua").equals(maLoai)){%>
                                        <option value="<%=rsLoaiSua.getString("ma_loai_sua")%>" selected><%=rsLoaiSua.getString("ten_loai")%></option>
                                    <%}else{%>
                                        <option value="<%=rsLoaiSua.getString("ma_loai_sua")%>"><%=rsLoaiSua.getString("ten_loai")%></option>
                                    <%}%>
                                <%}%>
                            </select>
                            Hãng sữa:
                            <select name="cboHangSua">
                                <%while(rsHangSua.next()){%>
                                    <%if(rsHangSua.getString("ma_hang_sua").equals(maHang)){%>
                                        <option value="<%=rsHangSua.getString("ma_hang_sua")%>" selected><%=rsHangSua.getString("ten_hang_sua")%></option>
                                    <%}else{%>
                                        <option value="<%=rsHangSua.getString("ma_hang_sua")%>"><%=rsHangSua.getString("ten_hang_sua")%></option>                                        
                                    <%}%>
                                <%}%>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            Tên sữa: <input type="text" name="txtTenSuaTim" value="">
                            <input type="submit" name="btnTimKiem" value="Tìm kiếm">
                        </td>
                    </tr>
                </tbody>
            </table>
        </form>
            <%if(soSanPham>0){%>
            <p>Có sản <%= soSanPham%> phẩm được tìm thấy</p>                
            <table border="1">
                <tbody>
                    <%while(rsSua.next()){%>
                    <tr>
                        <td colspan="2"><%=rsSua.getString("ten_sua")%>  </td>
                    </tr>
                    <tr>
                        <td><img src="images/<%=rsSua.getString("hinh")%>"></td>
                        <td>
                            <p><b>Thành phần dinh dưỡng</b></p>
                            <p><%=rsSua.getString("tp_dinh_duong")%></p>
                            <p><b>Lợi ích</b></p>
                            <p><%= rsSua.getString("loi_ich")%></p>
                            <p><b>Trọng lượng:</b> <%= rsSua.getInt("trong_luong")%> gram - <b>Đơn giá:</b> <%= nf.format(rsSua.getInt("don_gia"))%> VNĐ</p>
                        </td>
                    </tr>
                    <%}%>
                </tbody>
            </table>
            <%}%>
    </body>
</html>
