Imports System
Imports System.Windows
Imports System.Windows.Controls

Namespace MyCalculatorv1
    Public Partial Class MainWindow
        Inherits Window

        Public Sub New()
            Me.InitializeComponent()
        End Sub

        Private Sub Button_Click_1(ByVal sender As Object, ByVal e As RoutedEventArgs)
            'przycisk "B" jest przypisany calej grupie przyciskow ktorego wartosc jest rowna tekstowi zawartemu w "buttonie" , zaoszczedza to miejsca w kodzie
            Dim b = CType(sender, Button)
            Me.tb.Text += b.Content.ToString()
        End Sub
        'przycisk "wynikowy" "="
        Private Sub Result_click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Try
                result() 'wyswietlanie wyniku
            Catch __unusedException1__ As Exception
                Me.tb.Text = "Error!" 'jesli bedzie brak danych to pojawi sie error.
            End Try
        End Sub

        Private Sub result()
            Dim op As String
            Dim iOp = 0

            If Me.tb.Text.Contains("+") Then
                iOp = Me.tb.Text.IndexOf("+")
            ElseIf Me.tb.Text.Contains("-") Then
                iOp = Me.tb.Text.IndexOf("-")
            ElseIf Me.tb.Text.Contains("*") Then
                iOp = Me.tb.Text.IndexOf("*")
            ElseIf Me.tb.Text.Contains("/") Then
                iOp = Me.tb.Text.IndexOf("/")
            Else
                'blad  
            End If

            op = Me.tb.Text.Substring(iOp, 1)
            Dim op1 = Convert.ToDouble(Me.tb.Text.Substring(0, iOp))
            Dim op2 = Convert.ToDouble(Me.tb.Text.Substring(iOp + 1, Me.tb.Text.Length - iOp - 1))

            If Equals(op, "+") Then
                Me.tb.Text += "=" & op1 + op2
            ElseIf Equals(op, "-") Then
                Me.tb.Text += "=" & op1 - op2
            ElseIf Equals(op, "*") Then
                Me.tb.Text += "=" & op1 * op2
            Else
                Me.tb.Text += "=" & op1 / op2
            End If
        End Sub
        'Przycisk "Wyjdz" odpowiadajacy za wyjscie z programu
        Private Sub Off_Click_1(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Call Application.Current.Shutdown()
        End Sub
        'Tutaj jest przycisk "Del" , ma za zadanie usuwać całą zawartość pola z danymi
        Private Sub Del_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Me.tb.Text = ""
        End Sub
        ' Przycisk R odpowiada za usunięcie ostatniej cyfry tj."BackSpace"
        Private Sub R_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            If Me.tb.Text.Length > 0 Then
                Me.tb.Text = Me.tb.Text.Substring(0, Me.tb.Text.Length - 1)
            End If
        End Sub
        'tutaj jest pole w które będą "wstawiane" wyniki
        Private Sub tb_TextChanged(ByVal sender As Object, ByVal e As TextChangedEventArgs)
        End Sub
    End Class
End Namespace
