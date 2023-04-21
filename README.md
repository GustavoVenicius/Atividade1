# Atividade1
Repositorio para a atividade 1  GERENCIAMENTO DE CONFIGURAÇÃO DE SOFTWAREunit Calendario;

interface

uses
  SysUtils, WinTypes, WinProcs, Messages, Classes, Graphics, Controls,
  Forms, Dialogs, ExtCtrls, Grids, Calendar, StdCtrls, Buttons;

type
  TFrmCalendario = class(TForm)
    Calendar1: TCalendar;
    ThisDay: TLabel;
    Lyear: TBitBtn;
    Nyear: TBitBtn;
    LMonth: TBitBtn;
    NMonth: TBitBtn;
    Today: TBitBtn;
    procedure Calendar1Change(Sender: TObject);
    procedure NyearClick(Sender: TObject);
    procedure LyearClick(Sender: TObject);
    procedure NMonthClick(Sender: TObject);
    procedure LMonthClick(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure TodayClick(Sender: TObject);
    procedure FormClose(Sender: TObject; var Action: TCloseAction);
    procedure FormKeyDown(Sender: TObject; var Key: Word;
      Shift: TShiftState);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  FrmCalendario: TFrmCalendario;

implementation

{$R *.DFM}

procedure TFrmCalendario.FormCreate(Sender: TObject);
begin
    Calendar1Change(Self);
end;


procedure TFrmCalendario.Calendar1Change(Sender: TObject);

const Dayof : array[1..7] of Byte=(6,7,8,9,10,4,5);

var FirstDate : Tdatetime;
    WeekNumber : integer;
    gly, glm, gld : word;

begin
DecodeDate(Calendar1.CalendarDate,gly,glm,gld);
FirstDate:=EncodeDate(gly,1,1);
WeekNumber:=(trunc(Calendar1.CalendarDate)-trunc(FirstDate) + DayOf[DayOfWeek(FirstDate)])div 7;


{ If anyone can show me how to get rid of the following
  2 if statements, I would appreciate it. Although they both do the job. }

if weeknumber > 52 then weeknumber:=1;
if weeknumber < 1 then weeknumber:=1;
Caption := 'Semana nº ' + IntToStr(WeekNumber);
ThisDay.Caption := FormatDateTime(LongDateFormat, Calendar1.CalendarDate);
end;

procedure TFrmCalendario.NyearClick(Sender: TObject);
begin
Calendar1.NextYear;
end;

procedure TFrmCalendario.LyearClick(Sender: TObject);
begin
Calendar1.PrevYear;
end;

procedure TFrmCalendario.NMonthClick(Sender: TObject);
begin
Calendar1.NextMonth;
end;

procedure TFrmCalendario.LMonthClick(Sender: TObject);
begin
Calendar1.PrevMonth;
end;



procedure TFrmCalendario.TodayClick(Sender: TObject);
var Year, Month, Day : Word;
begin

DecodeDate(Now, Year, Month, Day);

{ Set Day to 1, otherwise, when Month is set the calendar may
  try to highlight an invalid day - Month could be Feb, and
  day could be 31 }

Calendar1.Day := 1;
Calendar1.Year := Year;
Calendar1.Month := Month;
Calendar1.Day := Day;
end;

procedure TFrmCalendario.FormClose(Sender: TObject;
  var Action: TCloseAction);
begin
    Action := Cafree;
    FrmCalendario := nil;
end;

procedure TFrmCalendario.FormKeyDown(Sender: TObject; var Key: Word;
  Shift: TShiftState);
begin
    if Key = vk_escape then Close; 
end;

end.
